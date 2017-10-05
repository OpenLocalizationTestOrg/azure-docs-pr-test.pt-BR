---
title: "Consultar dados do armazenamento do Azure compatível com o HDFS - Azure HDInsight | Microsoft Docs"
description: "Aprenda a consultar dados do Armazenamento do Azure e do Azure Data Lake Store para armazenar os resultados da sua análise."
keywords: "armazenamento de blobs, hdfs, dados estruturados, dados não estruturados, data lake store, entrada do Hadoop, saída do Hadoop, armazenamento do hadoop, entrada do hdfs, saída do hdfs, armazenamento do hdfs, wasb do azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: a44c2b363f7ebb593b9a9c5bd9e0d4fc3b4c31bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="3b3fb-104">Usar o Armazenamento do Azure com clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b3fb-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="3b3fb-105">Para analisar dados no cluster HDInsight, você pode armazenar os dados no Armazenamento do Azure, no Azure Data Lake Store ou em ambos.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="3b3fb-106">As duas opções de armazenamento permitem que os clusters HDInsight usados para cálculo sejam excluídos com segurança sem que ocorra perda de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="3b3fb-107">O Hadoop dá suporte a uma noção do sistema de arquivos padrão.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-107">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="3b3fb-108">O sistema de arquivos padrão implica esquema e autoridade padrões.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-108">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="3b3fb-109">Ele também pode ser usado para resolver caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-109">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="3b3fb-110">Durante o processo de criação do cluster HDInsight, você pode especificar um contêiner de blobs no Armazenamento do Azure como o sistema de arquivos padrão ou, com o HDInsight 3.5, você pode selecionar o Armazenamento do Azure ou o Azure Data Lake Store como o sistema de arquivos padrão com algumas exceções.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> <span data-ttu-id="3b3fb-111">Para o suporte do uso do Data Lake Store como o armazenamento padrão e o vinculado, veja [Disponibilidades para o cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-111">For the supportability of using Data Lake Store as both the default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="3b3fb-112">Neste artigo, você aprenderá como funciona o Armazenamento do Azure com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="3b3fb-113">Para saber como o Data Lake Store funciona com clusters HDInsight, veja [Usar o Azure Data Lake Store com clusters Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-113">To learn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="3b3fb-114">Para saber mais sobre a criação de um cluster HDInsight, veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="3b3fb-115">O Armazenamento do Azure é uma solução de armazenamento de uso geral que se integra perfeitamente com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="3b3fb-116">O HDInsight pode usar um contêiner de blobs no Armazenamento do Azure como o sistema de arquivos padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-116">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span></span> <span data-ttu-id="3b3fb-117">Através de uma interface HDFS (Sistema de Arquivos Distribuído Hadoop), o conjunto completo de componentes em HDInsight pode operar diretamente sobre os dados estruturados ou não estruturados armazenados como blobs.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-117">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="3b3fb-118">Há várias opções disponíveis ao criar uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="3b3fb-119">A tabela a seguir fornece informações sobre quais opções têm suporte com o HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-119">The following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="3b3fb-120">Tipo de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3b3fb-120">Storage account type</span></span> | <span data-ttu-id="3b3fb-121">Camada de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3b3fb-121">Storage tier</span></span> | <span data-ttu-id="3b3fb-122">Suporte com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b3fb-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="3b3fb-123">Conta de armazenamento de uso geral</span><span class="sxs-lookup"><span data-stu-id="3b3fb-123">General-purpose Storage Account</span></span> | <span data-ttu-id="3b3fb-124">Standard</span><span class="sxs-lookup"><span data-stu-id="3b3fb-124">Standard</span></span> | <span data-ttu-id="3b3fb-125">__Sim__</span><span class="sxs-lookup"><span data-stu-id="3b3fb-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="3b3fb-126">Premium</span><span class="sxs-lookup"><span data-stu-id="3b3fb-126">Premium</span></span> | <span data-ttu-id="3b3fb-127">Não</span><span class="sxs-lookup"><span data-stu-id="3b3fb-127">No</span></span> |
> | <span data-ttu-id="3b3fb-128">Conta de Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="3b3fb-128">Blob Storage Account</span></span> | <span data-ttu-id="3b3fb-129">Dinâmica</span><span class="sxs-lookup"><span data-stu-id="3b3fb-129">Hot</span></span> | <span data-ttu-id="3b3fb-130">Não</span><span class="sxs-lookup"><span data-stu-id="3b3fb-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="3b3fb-131">Estática</span><span class="sxs-lookup"><span data-stu-id="3b3fb-131">Cool</span></span> | <span data-ttu-id="3b3fb-132">Não</span><span class="sxs-lookup"><span data-stu-id="3b3fb-132">No</span></span> |

<span data-ttu-id="3b3fb-133">Não recomendamos o contêiner de blobs padrão para armazenar dados corporativos.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-133">We do not recommend that you use the default blob container for storing business data.</span></span> <span data-ttu-id="3b3fb-134">É uma prática recomendada excluir o contêiner de blobs padrão após cada uso para reduzir o custo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-134">Deleting the default blob container after each use to reduce storage cost is a good practice.</span></span> <span data-ttu-id="3b3fb-135">Observe que o contêiner padrão contém os logs do aplicativo e do sistema.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-135">Note that the default container contains application and system logs.</span></span> <span data-ttu-id="3b3fb-136">Certifique-se de recuperar os logs antes de excluir o contêiner.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-136">Make sure to retrieve the logs before deleting the container.</span></span>

<span data-ttu-id="3b3fb-137">Não há suporte para o compartilhamento de um contêiner de blobs para vários clusters.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="3b3fb-138">Arquitetura de armazenamento do HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b3fb-138">HDInsight storage architecture</span></span>
<span data-ttu-id="3b3fb-139">O diagrama a seguir fornece uma exibição abstrata da arquitetura de armazenamento do HDInsight de uso do Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-139">The following diagram provides an abstract view of the HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="3b3fb-140">![Clusters Hadoop usam a API HDFS para acessar e armazenar dados estruturados e não estruturados no armazenamento de blobs.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Arquitetura de Armazenamento do HDInsight")</span><span class="sxs-lookup"><span data-stu-id="3b3fb-140">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="3b3fb-141">O HDInsight fornece acesso ao sistema de arquivos distribuídos que está anexado localmente aos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-141">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span></span> <span data-ttu-id="3b3fb-142">Esse sistema de arquivos pode ser acessado usando o URI totalmente qualificado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-142">This file system can be accessed by using the fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="3b3fb-143">Além disso, o HDInsight permite que você acesse os dados armazenados no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-143">In addition, HDInsight allows you to access data that is stored in Azure Storage.</span></span> <span data-ttu-id="3b3fb-144">A sintaxe do é:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-144">The syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="3b3fb-145">Veja algumas considerações ao usar a conta de armazenamento do Azure com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="3b3fb-146">**Contêineres nas contas de armazenamento que estão conectadas a um cluster:** como o nome e a chave da conta são associados ao cluster durante a criação, você tem acesso completo aos blobs nesses contêineres.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-146">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span></span>

* <span data-ttu-id="3b3fb-147">**Contêineres públicos ou blobs públicos nas contas de armazenamento que NÃO estão conectadas a um cluster:** você tem permissão somente leitura para os blobs nos contêineres.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-147">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3b3fb-148">Um contêiner público permite obter uma lista de todos os blobs disponíveis nesse contêiner e obter metadados do contêiner.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-148">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="3b3fb-149">Um blob público somente permite acessar os blobs se você souber a URL exata.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-149">Public blobs allow you to access the blobs only if you know the exact URL.</span></span> <span data-ttu-id="3b3fb-150">Para saber mais, confira <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restringir o acesso a contêineres e blobs</a>.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="3b3fb-151">**Contêineres privados nas contas de armazenamento que NÃO estão conectadas a um cluster:** não é possível acessar os blobs nos contêineres, a menos que você defina a conta de armazenamento ao enviar os trabalhos do WebHCat.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-151">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span></span> <span data-ttu-id="3b3fb-152">Isso será explicado mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-152">This is explained later in this article.</span></span>

<span data-ttu-id="3b3fb-153">As contas de armazenamento definidas no processo de criação e suas chaves são armazenadas em %HADOOP_HOME%/conf/core-site.xml nos nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-153">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span></span> <span data-ttu-id="3b3fb-154">O comportamento padrão do HDInsight é usar as contas de armazenamento definidas no arquivo core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-154">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span></span> <span data-ttu-id="3b3fb-155">Você pode modificar essa configuração usando [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="3b3fb-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="3b3fb-156">Vários trabalhos do WebHCat, incluindo Hive, MapReduce, streaming de Hadoop e Pig, podem conter uma descrição de contas de armazenamento e metadados (normalmente funciona para Pig com contas de armazenamento, mas não para metadados).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="3b3fb-157">(Isso funciona atualmente com o Pig para contas de armazenamento, mas não para metadados.) Para obter mais informações, consulte [Usando um Cluster HDInsight com metastores e contas de armazenamento alternativas](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="3b3fb-158">Os blobs podem ser usados para dados estruturados e não estruturados.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="3b3fb-159">Os contêineres de blob armazenam dados como pares de chave/valor, e não há nenhuma hierarquia de diretório.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="3b3fb-160">No entanto, o caractere "/" pode ser usado dentro do nome de chave para parecer que um arquivo está armazenado em uma estrutura de diretório.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-160">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="3b3fb-161">Por exemplo, a chave de um blob pode ser *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="3b3fb-162">Não existe nenhum diretório de *entrada* real, mas, devido à presença do caractere "/" no nome da chave, ele parece um caminho de arquivo.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-162">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span></span>

## <span data-ttu-id="3b3fb-163"><a id="benefits"></a>Benefícios do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3b3fb-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="3b3fb-164">O custo de desempenho implícito de não ter clusters de cálculo e recursos de armazenamento colocalizados é reduzido pela forma como os clusters de cálculo são criados próximos aos recursos da conta de armazenamento na região do Azure, no qual a rede de alta velocidade torna os nós de computação eficientes para acessarem os dados no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-164">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it efficient for the compute nodes to access the data inside Azure storage.</span></span>

<span data-ttu-id="3b3fb-165">Há vários benefícios associados ao armazenamento de dados no Armazenamento do Azure em vez de no HDFS:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-165">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="3b3fb-166">**Compartilhamento e reutilização de dados:** os dados no HDFS estão localizados dentro do cluster de computação.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-166">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span></span> <span data-ttu-id="3b3fb-167">Apenas os aplicativos que têm acesso ao cluster de computação podem usar os dados usando a API HDFS.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-167">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span></span> <span data-ttu-id="3b3fb-168">Os dados no Armazenamento do Azure podem ser acessados por meio de APIs HDFS ou por meio de [APIs REST do Armazenamento de Blobs][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="3b3fb-168">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="3b3fb-169">Assim, um conjunto maior de aplicativos (incluindo outros clusters HDInsight) e ferramentas podem ser usados para produzir e consumir os dados.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span></span>
* <span data-ttu-id="3b3fb-170">**Arquivamento de dados:** o armazenamento de dados no Armazenamento do Azure permite que os clusters HDInsight usados para cálculo sejam excluídos com segurança sem que ocorra perda de dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-170">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span></span>
* <span data-ttu-id="3b3fb-171">**Custo do armazenamento de dados:** o armazenamento de dados no DFS a longo prazo é mais caro do que o armazenamento de dados no Armazenamento do Azure, uma vez que o custo de um cluster de computação é mais alto do que o custo do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-171">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span></span> <span data-ttu-id="3b3fb-172">Além disso, como os dados não precisam ser recarregados para cada geração de cluster de computação, você está economizando em custos de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-172">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="3b3fb-173">**Escala horizontal elástica:** embora o HDFS forneça um sistema de arquivos escalado horizontalmente, a escala é determinada pelo número de nós que você cria para o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span></span> <span data-ttu-id="3b3fb-174">A alteração da escala pode se tornar um processo mais complicado do que depender dos recursos de dimensionamento elástico do Armazenamento do Azure que você obtém automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-174">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="3b3fb-175">**Replicação geográfica:** seu Armazenamento do Azure pode ser replicado geograficamente.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="3b3fb-176">Embora isso forneça redundância de dados e recuperação geográfica, um failover para o local replicado geograficamente afetará seriamente o desempenho e poderá incorrer em custos adicionais.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-176">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="3b3fb-177">Portanto, nossa recomendação é escolher a replicação geográfica com sabedoria e somente se o valor dos dados compensar o custo adicional.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-177">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span></span>

<span data-ttu-id="3b3fb-178">Determinados trabalhos e pacotes do MapReduce podem criar resultados intermediários que você não deseja realmente armazenar no contêiner de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span></span> <span data-ttu-id="3b3fb-179">Nesse caso, você ainda pode optar por armazenar os dados no HDFS local.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-179">In that case, you can elect to store the data in the local HDFS.</span></span> <span data-ttu-id="3b3fb-180">Na verdade, o HDInsight usa o DFS para vários desses resultados intermediários em trabalhos Hive e outros processos.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3fb-181">A maioria dos comandos HDFS (como <b>ls</b>, <b>copyFromLocal</b> e <b>mkdir</b>) ainda funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="3b3fb-182">Apenas os comandos específicos à implementação nativa do HDFS (que é conhecida como DFS), como <b>fschk</b> e <b>dfsadmin</b> mostram um comportamento diferente no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-182">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="3b3fb-183">Criar contêineres de blob</span><span class="sxs-lookup"><span data-stu-id="3b3fb-183">Create Blob containers</span></span>
<span data-ttu-id="3b3fb-184">Para usar blobs, primeiro você deve criar uma [conta de armazenamento do Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="3b3fb-184">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="3b3fb-185">Como parte desse processo, especifique uma região do Azure na qual a conta de armazenamento será criada.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-185">As part of this, you specify an Azure region where the storage account is created.</span></span> <span data-ttu-id="3b3fb-186">O cluster e a conta de armazenamento devem ser hospedados na mesma região.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-186">The cluster and the storage account must be hosted in the same region.</span></span> <span data-ttu-id="3b3fb-187">O banco de dados SQL Server do metastore do Hive e o banco de dados SQL do metastore do Oozie também devem estar localizados na mesma região.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-187">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span></span>

<span data-ttu-id="3b3fb-188">Independentemente de onde estiverem, cada blob que você criar pertencerá a um contêiner na sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-188">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span></span> <span data-ttu-id="3b3fb-189">Esse contêiner pode ser um contêiner de armazenamento de blob existente criado fora do HDInsight, ou pode ser um contêiner criado para um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="3b3fb-190">O contêiner de blob padrão armazena informações específicas do cluster como logs e o histórico do trabalho.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-190">The default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="3b3fb-191">Não compartilhe um contêiner de armazenamento de blob padrão com vários clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="3b3fb-192">Isso pode corromper o histórico de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-192">This might corrupt job history.</span></span> <span data-ttu-id="3b3fb-193">É recomendável usar um contêiner diferente para cada cluster e colocar os dados compartilhados em uma conta de armazenamento vinculada especificada na implantação de todos os clusters relevantes, e não na conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-193">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span></span> <span data-ttu-id="3b3fb-194">Para obter mais informações sobre como configurar contas de armazenamento vinculadas, veja [Criar clusters HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="3b3fb-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="3b3fb-195">No entanto, você pode reutilizar um contêiner de armazenamento padrão depois que o cluster HDInsight original for excluído.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-195">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="3b3fb-196">Para clusters HBase, você pode realmente manter os dados e o esquema de tabela do HBase criando um novo cluster HBase com o contêiner de blobs padrão usado por um cluster HBase que foi excluído.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-196">For HBase clusters, you can actually retain the HBase table schema and data by creating a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-the-azure-portal"></a><span data-ttu-id="3b3fb-197">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3b3fb-197">Use the Azure portal</span></span>
<span data-ttu-id="3b3fb-198">Ao criar um cluster HDInsight no Portal, você tem as opções (como mostrado abaixo) para fornecer os detalhes da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-198">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span></span> <span data-ttu-id="3b3fb-199">Você também pode especificar se deseja uma conta de armazenamento adicional associada ao cluster e, em caso afirmativo, escolher entre o Data Lake Store ou outro Azure Storage Blob como o armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-199">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span></span>

![Fonte de dados de criação do hadoop do HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="3b3fb-201">Não há suporte para o uso de uma conta de armazenamento adicional em um local diferente do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-201">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="3b3fb-202">Usar PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="3b3fb-202">Use Azure PowerShell</span></span>
<span data-ttu-id="3b3fb-203">Se você tiver [instalado e configurado o Azure PowerShell][powershell-install], poderá usar o seguinte no prompt do Azure PowerShell para criar uma conta de armazenamento e o contêiner:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-203">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="3b3fb-204">Usar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3b3fb-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="3b3fb-205">Se você tiver [instalado e configurado a CLI do Azure](../cli-install-nodejs.md), o comando a seguir pode ser usado para uma conta de armazenamento e o contêiner.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-205">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="3b3fb-206">O parâmetro `--type` indica como a conta de armazenamento é replicada.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-206">The `--type` parameter indicates how the storage account is replicated.</span></span> <span data-ttu-id="3b3fb-207">Para saber mais, veja [Replicação do Armazenamento do Azure](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="3b3fb-208">Não use ZRS, pois o ZRS não dá suporte ao blob de páginas, arquivo, tabela ou fila.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="3b3fb-209">Você recebe uma solicitação para especificar a região geográfica na qual a conta de armazenamento é criada.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-209">You are prompted to specify the geographic region that the storage account is created in.</span></span> <span data-ttu-id="3b3fb-210">Você deve criar a conta de armazenamento na mesma região em que pretende criar o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-210">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="3b3fb-211">Assim que a conta de armazenamento for criada, use o seguinte comando para recuperar as chaves de conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-211">Once the storage account is created, use the following command to retrieve the storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="3b3fb-212">Para criar um novo contêiner, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-212">To create a container, use the following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="3b3fb-213">Arquivos de endereços no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3b3fb-213">Address files in Azure storage</span></span>
<span data-ttu-id="3b3fb-214">O esquema de URI para acessar arquivos no Armazenamento do Azure pelo HDInsight é:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-214">The URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="3b3fb-215">O esquema de URI fornece acesso sem criptografia (com o prefixo *wasb:*) e acesso criptografado SSL (com *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-215">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="3b3fb-216">Recomendamos usar *wasbs* sempre que possível, mesmo ao acessar dados que residem dentro da mesma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span></span>

<span data-ttu-id="3b3fb-217">O &lt;BlobStorageContainerName&gt; identifica o nome do contêiner de blobs no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-217">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span></span>
<span data-ttu-id="3b3fb-218">O &lt;StorageAccountName&gt; identifica o nome da conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-218">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span></span> <span data-ttu-id="3b3fb-219">Um FQDN (nome de domínio totalmente qualificado) é necessário.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="3b3fb-220">Se nem &lt;BlobStorageContainerName&gt; nem &lt;StorageAccountName&gt; for especificado, o sistema de arquivos padrão será usado.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span></span> <span data-ttu-id="3b3fb-221">Para os arquivos no sistema de arquivos padrão, você pode usar um caminho absoluto ou um caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-221">For the files on the default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="3b3fb-222">Por exemplo, o arquivo *hadoop-mapreduce-examples.jar* fornecido com clusters HDInsight pode ser referenciado para usar um dos seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-222">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="3b3fb-223">O nome do arquivo é <i>hadoop-examples.jar</i> em clusters HDInsight versões 2.1 e 1.6.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-223">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="3b3fb-224">O &lt;path&gt; é o nome do caminho do HDFS do arquivo ou do diretório.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-224">The &lt;path&gt; is the file or directory HDFS path name.</span></span> <span data-ttu-id="3b3fb-225">Como os contêineres no Armazenamento do Azure são apenas um repositório de chave-valor, não há nenhum sistema de arquivos hierárquico verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="3b3fb-226">Um caractere "/" dentro de uma chave de blob é interpretado como um separador de diretório.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="3b3fb-227">Por exemplo, o nome do blob para *hadoop-mapreduce-examples.jar* é:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-227">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="3b3fb-228">Ao trabalhar com blobs fora do HDInsight, a maioria dos utilitários não reconhecem o formato WASB e, em vez disso, esperam um formato de caminho básico, como `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-228">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="3b3fb-229">Acessar blobs</span><span class="sxs-lookup"><span data-stu-id="3b3fb-229">Access blobs</span></span> 


### <span data-ttu-id="3b3fb-230"><a name="access-blobs-using-azure-powershell"></a> Usar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b3fb-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="3b3fb-231">Os comandos nesta seção fornecem um exemplo básico de como usar o PowerShell para acessar dados armazenados em blobs.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span></span> <span data-ttu-id="3b3fb-232">Para obter um exemplo mais completo que é personalizado para trabalhar com o HDInsight, consulte as [Ferramentas do HDInsight](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="3b3fb-233">Use o seguinte comando para listar os cmdlets relacionados ao blob:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-233">Use the following command to list the blob-related cmdlets:</span></span>

    Get-Command *blob*

![Lista de cmdlets do PowerShell relacionados ao blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="3b3fb-235">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="3b3fb-235">Upload files</span></span>
<span data-ttu-id="3b3fb-236">Veja [Carregar dados no HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="3b3fb-236">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="3b3fb-237">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="3b3fb-237">Download files</span></span>
<span data-ttu-id="3b3fb-238">O script a seguir baixa um blob de blocos na pasta atual.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-238">The following script downloads a block blob to the current folder.</span></span> <span data-ttu-id="3b3fb-239">Antes de executar o script, altere o diretório de uma pasta na qual você tenha permissão de gravação.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-239">Before running the script, change the directory to a folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # The storage account used for the default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # The default file system container has the same name as the cluster.
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    # Use Add-AzureAccount if you haven't connected to your Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List the downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="3b3fb-240">Ao fornecer o nome do grupo de recursos e o nome do cluster, é possível usar o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-240">Providing the resource group name and the cluster name, you can use the following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="3b3fb-241">Excluir arquivos</span><span class="sxs-lookup"><span data-stu-id="3b3fb-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="3b3fb-242">Listar arquivos</span><span class="sxs-lookup"><span data-stu-id="3b3fb-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="3b3fb-243">Executar consultas do Hive usando uma conta de armazenamento indefinida</span><span class="sxs-lookup"><span data-stu-id="3b3fb-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="3b3fb-244">Este exemplo mostra como listar uma pasta em uma conta de armazenamento que não é definida durante o processo de criação.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span></span>
<span data-ttu-id="3b3fb-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="3b3fb-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="3b3fb-246">Usar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3b3fb-246">Use Azure CLI</span></span>
<span data-ttu-id="3b3fb-247">Use o comando a seguir para listar os comandos relacionados ao blob:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-247">Use the following command to list the blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="3b3fb-248">**Exemplo de como usar a CLI do Azure para carregar um arquivo**</span><span class="sxs-lookup"><span data-stu-id="3b3fb-248">**Example of using Azure CLI to upload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="3b3fb-249">**Exemplo de como usar a CLI do Azure para baixar um arquivo**</span><span class="sxs-lookup"><span data-stu-id="3b3fb-249">**Example of using Azure CLI to download a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="3b3fb-250">**Exemplo de como usar a CLI do Azure para excluir um arquivo**</span><span class="sxs-lookup"><span data-stu-id="3b3fb-250">**Example of using Azure CLI to delete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="3b3fb-251">**Exemplo de como usar a CLI do Azure para listar arquivos**</span><span class="sxs-lookup"><span data-stu-id="3b3fb-251">**Example of using Azure CLI to list files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="3b3fb-252">Usar contas de armazenamento adicionais</span><span class="sxs-lookup"><span data-stu-id="3b3fb-252">Use additional storage accounts</span></span>

<span data-ttu-id="3b3fb-253">Ao criar um cluster HDInsight, você especifica a conta de armazenamento do Azure que deseja associar a ele.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-253">While creating an HDInsight cluster, you specify the Azure Storage account you want to associate with it.</span></span> <span data-ttu-id="3b3fb-254">Além dessa conta de armazenamento, você pode adicionar mais contas de armazenamento da mesma assinatura do Azure ou de diferentes assinaturas do Azure durante o processo de criação ou após a criação de um cluster.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-254">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span></span> <span data-ttu-id="3b3fb-255">Para obter instruções sobre como adicionar mais contas de armazenamento, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="3b3fb-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="3b3fb-256">Não há suporte para o uso de uma conta de armazenamento adicional em um local diferente do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-256">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b3fb-257">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b3fb-257">Next steps</span></span>
<span data-ttu-id="3b3fb-258">Neste artigo, você aprendeu a usar o armazenamento do Azure compatível com HDFS com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-258">In this article, you learned how to use HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="3b3fb-259">Isso permite que você crie soluções de aquisição de dados para arquivamento de longo prazo escalonáveis e use o HDInsight para desbloquear as informações nos dados armazenados estruturados e não estruturados.</span><span class="sxs-lookup"><span data-stu-id="3b3fb-259">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="3b3fb-260">Para obter mais informações, confira:</span><span class="sxs-lookup"><span data-stu-id="3b3fb-260">For more information, see:</span></span>

* <span data-ttu-id="3b3fb-261">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="3b3fb-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="3b3fb-262">Introdução ao Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3b3fb-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="3b3fb-263">[Carregar dados no HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="3b3fb-263">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="3b3fb-264">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="3b3fb-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="3b3fb-265">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3b3fb-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="3b3fb-266">[Usar Assinaturas de Acesso Compartilhado do Armazenamento do Azure para restringir o acesso a dados com o HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="3b3fb-266">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
