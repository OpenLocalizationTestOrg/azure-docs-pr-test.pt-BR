---
title: "dados aaaQuery do HDFS compatível com o armazenamento do Azure - HDInsight do Azure | Microsoft Docs"
description: "Saiba como os dados de tooquery do armazenamento do Azure e do repositório Azure Data Lake toostore resultados da análise."
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
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="b541f-104">Usar o Armazenamento do Azure com clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="b541f-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="b541f-105">dados tooanalyze no cluster HDInsight, você pode armazenar dados de saudação no armazenamento do Azure, o repositório Azure Data Lake ou ambos.</span><span class="sxs-lookup"><span data-stu-id="b541f-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="b541f-106">Ambas as opções de armazenamento permitem que você exclua toosafely clusters de HDInsight que são usados para a computação sem perda de dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="b541f-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="b541f-107">Hadoop oferece suporte a uma noção saudação padrão do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b541f-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="b541f-108">sistema de arquivos padrão Olá implica um esquema padrão e uma autoridade.</span><span class="sxs-lookup"><span data-stu-id="b541f-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="b541f-109">Ele também pode ser usado tooresolve os caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="b541f-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="b541f-110">Durante a saudação o processo de criação de cluster HDInsight, você pode especificar um contêiner de blob no armazenamento do Azure como sistema de arquivos padrão hello ou com HDInsight 3.5, você pode selecionar armazenamento do Azure ou repositório Azure Data Lake como sistema de arquivos padrão Olá com algumas exceções.</span><span class="sxs-lookup"><span data-stu-id="b541f-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="b541f-111">Para dar suporte a saudação de usando o repositório Data Lake como saudação padrão e vinculado de armazenamento, consulte [Availabilities para cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="b541f-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="b541f-112">Neste artigo, você aprenderá como funciona o Armazenamento do Azure com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="b541f-113">toolearn como repositório Data Lake funciona com clusters de HDInsight, consulte [clusters do repositório Azure Data Lake uso com o Azure HDInsight](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="b541f-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="b541f-114">Para saber mais sobre a criação de um cluster HDInsight, veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b541f-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="b541f-115">O Armazenamento do Azure é uma solução de armazenamento de uso geral que se integra perfeitamente com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="b541f-116">HDInsight pode usar um contêiner de blob no armazenamento do Azure como sistema de arquivos padrão Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b541f-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="b541f-117">Através de uma interface de (HDFS) do sistema de arquivos distribuído Hadoop, todo o conjunto de componentes em HDInsight Olá pode operar diretamente nos dados estruturados ou não estruturados armazenados como blobs.</span><span class="sxs-lookup"><span data-stu-id="b541f-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="b541f-118">Há várias opções disponíveis ao criar uma conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="b541f-119">Olá, a tabela a seguir fornece informações sobre quais opções são suportadas com HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b541f-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="b541f-120">Tipo de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b541f-120">Storage account type</span></span> | <span data-ttu-id="b541f-121">Camada de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b541f-121">Storage tier</span></span> | <span data-ttu-id="b541f-122">Suporte com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="b541f-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="b541f-123">Conta de armazenamento de uso geral</span><span class="sxs-lookup"><span data-stu-id="b541f-123">General-purpose Storage Account</span></span> | <span data-ttu-id="b541f-124">Standard</span><span class="sxs-lookup"><span data-stu-id="b541f-124">Standard</span></span> | <span data-ttu-id="b541f-125">__Sim__</span><span class="sxs-lookup"><span data-stu-id="b541f-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="b541f-126">Premium</span><span class="sxs-lookup"><span data-stu-id="b541f-126">Premium</span></span> | <span data-ttu-id="b541f-127">Não</span><span class="sxs-lookup"><span data-stu-id="b541f-127">No</span></span> |
> | <span data-ttu-id="b541f-128">Conta de Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="b541f-128">Blob Storage Account</span></span> | <span data-ttu-id="b541f-129">Dinâmica</span><span class="sxs-lookup"><span data-stu-id="b541f-129">Hot</span></span> | <span data-ttu-id="b541f-130">Não</span><span class="sxs-lookup"><span data-stu-id="b541f-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="b541f-131">Estática</span><span class="sxs-lookup"><span data-stu-id="b541f-131">Cool</span></span> | <span data-ttu-id="b541f-132">Não</span><span class="sxs-lookup"><span data-stu-id="b541f-132">No</span></span> |

<span data-ttu-id="b541f-133">Não é recomendável que você use o contêiner de blob saudação padrão para armazenar dados de negócios.</span><span class="sxs-lookup"><span data-stu-id="b541f-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="b541f-134">Excluindo contêiner de blob padrão Olá depois de cada tooreduce use o custo de armazenamento é uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="b541f-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="b541f-135">Observação contêiner saudação padrão contém o aplicativo e sistema de logs.</span><span class="sxs-lookup"><span data-stu-id="b541f-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="b541f-136">Verifique tooretrieve-se de que logs de saudação antes de excluir o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="b541f-137">Não há suporte para o compartilhamento de um contêiner de blobs para vários clusters.</span><span class="sxs-lookup"><span data-stu-id="b541f-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="b541f-138">Arquitetura de armazenamento do HDInsight</span><span class="sxs-lookup"><span data-stu-id="b541f-138">HDInsight storage architecture</span></span>
<span data-ttu-id="b541f-139">Olá diagrama a seguir fornece uma exibição abstrata de saudação HDInsight a arquitetura de armazenamento do uso do armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="b541f-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="b541f-140">![Clusters de Hadoop usam Olá HDFS API tooaccess e armazenam dados estruturados e no armazenamento de Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Arquitetura de armazenamento do HDInsight")</span><span class="sxs-lookup"><span data-stu-id="b541f-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="b541f-141">HDInsight fornece acesso toohello distribuída arquivo sistema localmente anexado toohello nós de computação.</span><span class="sxs-lookup"><span data-stu-id="b541f-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="b541f-142">Este sistema de arquivos pode ser acessado usando Olá totalmente qualificado URI, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b541f-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="b541f-143">Além disso, HDInsight permite tooaccess dados armazenados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="b541f-144">Olá sintaxe é:</span><span class="sxs-lookup"><span data-stu-id="b541f-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="b541f-145">Veja algumas considerações ao usar a conta de armazenamento do Azure com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="b541f-146">**Contêineres em contas de armazenamento Olá tooa conectado de cluster:** porque Olá nome de conta e chave estão associados com cluster Olá durante a criação, você tem blobs toohello acesso completo esses contêineres.</span><span class="sxs-lookup"><span data-stu-id="b541f-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="b541f-147">**Contêineres do públicos ou blobs públicos em contas de armazenamento que não estão conectados cluster tooa:** , você tem permissão somente leitura toohello blobs em contêineres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="b541f-148">Contêineres do públicos permitem que você tooget uma lista de todos os blobs que estão disponíveis no contêiner e obter metadados do contêiner.</span><span class="sxs-lookup"><span data-stu-id="b541f-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="b541f-149">Blobs públicos permitem blobs de saudação tooaccess somente se você souber a URL exata hello.</span><span class="sxs-lookup"><span data-stu-id="b541f-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="b541f-150">Para obter mais informações, consulte <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">restringir acesso toocontainers e blobs</a>.</span><span class="sxs-lookup"><span data-stu-id="b541f-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="b541f-151">**Contêineres privados em contas de armazenamento que não estão conectados cluster tooa:** você não pode acessar blobs Olá em contêineres hello, a menos que você definir conta de armazenamento hello quando você enviar trabalhos de WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="b541f-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="b541f-152">Isso será explicado mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b541f-152">This is explained later in this article.</span></span>

<span data-ttu-id="b541f-153">contas de armazenamento de saudação que são definidas no processo de criação de saudação e suas chaves são armazenadas no %HADOOP_HOME%/conf/core-site.xml em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="b541f-154">comportamento padrão de saudação do HDInsight é toouse contas de armazenamento de saudação definidas no arquivo de Core-site.XML hello.</span><span class="sxs-lookup"><span data-stu-id="b541f-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="b541f-155">Você pode modificar essa configuração usando [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="b541f-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="b541f-156">Vários trabalhos do WebHCat, incluindo Hive, MapReduce, streaming de Hadoop e Pig, podem conter uma descrição de contas de armazenamento e metadados (normalmente funciona para Pig com contas de armazenamento, mas não para metadados).</span><span class="sxs-lookup"><span data-stu-id="b541f-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="b541f-157">(Isso funciona atualmente com o Pig para contas de armazenamento, mas não para metadados.) Para obter mais informações, consulte [Usando um Cluster HDInsight com metastores e contas de armazenamento alternativas](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="b541f-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="b541f-158">Os blobs podem ser usados para dados estruturados e não estruturados.</span><span class="sxs-lookup"><span data-stu-id="b541f-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="b541f-159">Os contêineres de blob armazenam dados como pares de chave/valor, e não há nenhuma hierarquia de diretório.</span><span class="sxs-lookup"><span data-stu-id="b541f-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="b541f-160">No entanto, caractere de barra (/) do hello pode ser usado em Olá toomake de nome da chave, ele aparece como se um arquivo é armazenado em uma estrutura de diretório.</span><span class="sxs-lookup"><span data-stu-id="b541f-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="b541f-161">Por exemplo, a chave de um blob pode ser *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="b541f-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="b541f-162">Não real *entrada* diretório existe, mas devido a presença de toohello de caractere de barra Olá no nome da chave hello, ele tem aparência de saudação de um caminho de arquivo.</span><span class="sxs-lookup"><span data-stu-id="b541f-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="b541f-163"><a id="benefits"></a>Benefícios do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b541f-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="b541f-164">Olá implícita custo de desempenho de recursos de armazenamento e clusters de computação não compartilhando mitigado pela maneira Olá clusters de computação de saudação são criados os recursos de conta de armazenamento toohello fechar dentro Olá região do Azure, em rede de alta velocidade Olá faz eficiente para nós de computação Olá tooaccess Olá dados dentro do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="b541f-165">Há vários benefícios associados ao armazenamento de dados de saudação no armazenamento do Azure, em vez de HDFS:</span><span class="sxs-lookup"><span data-stu-id="b541f-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="b541f-166">**Compartilhamento e reutilização de dados:** dados Olá no HDFS estão localizados dentro do cluster de computação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="b541f-167">Somente aplicativos Olá que têm acesso toohello compute cluster pode usar dados de saudação por meio de APIs de HDFS.</span><span class="sxs-lookup"><span data-stu-id="b541f-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="b541f-168">dados de saudação no armazenamento do Azure podem ser acessados por meio de saudação APIs HDFS ou Olá [APIs de REST do armazenamento de Blob][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="b541f-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="b541f-169">Assim, um conjunto maior de aplicativos (incluindo outros clusters de HDInsight) e ferramentas pode ser usado tooproduce e consumir dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="b541f-170">**Arquivamento de dados:** armazenar dados no armazenamento do Azure permite que os clusters de HDInsight Olá usados para computação toobe excluído com segurança sem perda de dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="b541f-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="b541f-171">**Custo de armazenamento de dados:** armazenando dados em DFS de longo prazo de saudação é mais caro do que armazenar dados saudação no armazenamento do Azure, porque o custo de saudação de um cluster de computação é maior do que o custo de saudação do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="b541f-172">Além disso, como dados de saudação não têm toobe recarregado para cada geração de cluster de computação, você está salvando também os custos de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="b541f-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="b541f-173">**Expansão elástica:** HDFS embora fornece um sistema de arquivos expandido, escala Olá é determinada pelo número de saudação de nós que você cria para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b541f-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="b541f-174">Alterar escala Olá pode se tornar um processo mais complicado que depender elástica hello dimensionar os recursos que você obtém automaticamente no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="b541f-175">**Replicação geográfica:** seu Armazenamento do Azure pode ser replicado geograficamente.</span><span class="sxs-lookup"><span data-stu-id="b541f-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="b541f-176">Embora isso fornece recuperação geográfica e a redundância de dados, um failover toohello replicado geograficamente local severos afeta o desempenho e ele pode incorrer em custos adicionais.</span><span class="sxs-lookup"><span data-stu-id="b541f-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="b541f-177">Portanto, nossa recomendação é toochoose Olá da replicação geográfica cuidadosamente e somente se o valor Olá dados saudação vale a pena custo adicional de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="b541f-178">Determinados trabalhos MapReduce e os pacotes podem criar resultados intermediários que você não deseja realmente toostore no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="b541f-179">Nesse caso, você pode decidir dados Olá toostore Olá HDFS local.</span><span class="sxs-lookup"><span data-stu-id="b541f-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="b541f-180">Na verdade, o HDInsight usa o DFS para vários desses resultados intermediários em trabalhos Hive e outros processos.</span><span class="sxs-lookup"><span data-stu-id="b541f-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="b541f-181">A maioria dos comandos HDFS (como <b>ls</b>, <b>copyFromLocal</b> e <b>mkdir</b>) ainda funciona conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="b541f-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="b541f-182">Olá somente os comandos que são específicos de toohello HDFS implementação nativa (que é chamado tooas DFS), como <b>fschk</b> e <b>dfsadmin</b>, mostrar um comportamento diferente no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="b541f-183">Criar contêineres de blob</span><span class="sxs-lookup"><span data-stu-id="b541f-183">Create Blob containers</span></span>
<span data-ttu-id="b541f-184">toouse blobs, primeiro você cria um [conta de armazenamento do Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="b541f-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="b541f-185">Como parte disso, você deve especificar uma região do Azure em que a conta de armazenamento de saudação é criada.</span><span class="sxs-lookup"><span data-stu-id="b541f-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="b541f-186">cluster Hello e conta de armazenamento Olá devem ser hospedados em Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="b541f-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="b541f-187">banco de dados do SQL Server metastore Olá Hive e Oozie metastore também deve estar localizado do banco de dados do SQL Server Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="b541f-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="b541f-188">Independentemente de onde ele reside, cada blob que você criar pertence tooa contêiner na sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="b541f-189">Esse contêiner pode ser um contêiner de armazenamento de blob existente criado fora do HDInsight, ou pode ser um contêiner criado para um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="b541f-190">contêiner de Blob padrão Olá armazena informações específicas do cluster, como logs e o histórico de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b541f-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="b541f-191">Não compartilhe um contêiner de armazenamento de blob padrão com vários clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="b541f-192">Isso pode corromper o histórico de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="b541f-192">This might corrupt job history.</span></span> <span data-ttu-id="b541f-193">É recomendável toouse um contêiner diferente para cada cluster e colocar os dados compartilhados em uma conta de armazenamento vinculado especificada na implantação de todos os clusters, em vez da conta de armazenamento padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="b541f-194">Para obter mais informações sobre como configurar contas de armazenamento vinculadas, veja [Criar clusters HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="b541f-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="b541f-195">No entanto, você pode reutilizar um contêiner de armazenamento padrão depois que o cluster HDInsight original de saudação foi excluído.</span><span class="sxs-lookup"><span data-stu-id="b541f-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="b541f-196">Para clusters do HBase, você poderá manter, na verdade, dados e esquema de tabela do HBase Olá criando um novo cluster HBase usando o contêiner de blob do saudação padrão que é usado por um cluster HBase que foi excluído.</span><span class="sxs-lookup"><span data-stu-id="b541f-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="b541f-197">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b541f-197">Use hello Azure portal</span></span>
<span data-ttu-id="b541f-198">Ao criar um cluster HDInsight do hello Portal, você tem detalhes da conta de armazenamento tooprovide Olá Olá opções (conforme mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="b541f-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="b541f-199">Você também pode especificar se deseja que uma conta de armazenamento adicionais associados cluster hello e, nesse caso, escolha de repositório Data Lake ou outro blob de armazenamento do Azure como armazenamento adicional da saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![Fonte de dados de criação do hadoop do HDInsight](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="b541f-201">Não há suporte para usando uma conta de armazenamento adicional no cluster do HDInsight Olá um local diferente.</span><span class="sxs-lookup"><span data-stu-id="b541f-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="b541f-202">Usar PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="b541f-202">Use Azure PowerShell</span></span>
<span data-ttu-id="b541f-203">Se você [instalado e configurado o Azure PowerShell][powershell-install], você pode usar o hello a seguir de saudação do Azure PowerShell prompt toocreate uma conta de armazenamento e o contêiner:</span><span class="sxs-lookup"><span data-stu-id="b541f-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

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

### <a name="use-azure-cli"></a><span data-ttu-id="b541f-204">Usar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b541f-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="b541f-205">Se você tiver [instalado e configurado Olá CLI do Azure](../cli-install-nodejs.md), seguinte Olá comando pode ser usado tooa conta de armazenamento e contêiner.</span><span class="sxs-lookup"><span data-stu-id="b541f-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="b541f-206">Olá `--type` parâmetro indica como a conta de armazenamento Olá é replicada.</span><span class="sxs-lookup"><span data-stu-id="b541f-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="b541f-207">Para saber mais, veja [Replicação do Armazenamento do Azure](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="b541f-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="b541f-208">Não use ZRS, pois o ZRS não dá suporte ao blob de páginas, arquivo, tabela ou fila.</span><span class="sxs-lookup"><span data-stu-id="b541f-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="b541f-209">Você está toospecify solicitadas Olá região geográfica que Olá conta de armazenamento é criada no.</span><span class="sxs-lookup"><span data-stu-id="b541f-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="b541f-210">Você deve criar a conta de armazenamento Olá no hello mesma região que você planeja criar seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="b541f-211">Depois de criar a conta de armazenamento Olá, use Olá chaves de conta de armazenamento do comando tooretrieve Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b541f-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="b541f-212">toocreate um contêiner, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b541f-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="b541f-213">Arquivos de endereços no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b541f-213">Address files in Azure storage</span></span>
<span data-ttu-id="b541f-214">Olá esquema URI para acessar arquivos no armazenamento do Azure do HDInsight é:</span><span class="sxs-lookup"><span data-stu-id="b541f-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="b541f-215">o esquema de URI Olá fornece acesso não criptografado (com hello *wasb:* prefixo) e SSL criptografadas acesso (com *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="b541f-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="b541f-216">É recomendável usar *wasbs* sempre que possível, mesmo quando o acesso a dados que residem dentro de Olá mesma região no Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="b541f-217">Olá &lt;BlobStorageContainerName&gt; identifica nome Olá Olá do contêiner de blob no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b541f-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="b541f-218">Olá &lt;StorageAccountName&gt; identifica o nome de conta de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b541f-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="b541f-219">Um FQDN (nome de domínio totalmente qualificado) é necessário.</span><span class="sxs-lookup"><span data-stu-id="b541f-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="b541f-220">Se nem &lt;BlobStorageContainerName&gt; nem &lt;StorageAccountName&gt; tiver sido especificado, sistema de arquivos padrão de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="b541f-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="b541f-221">Para arquivos Olá no sistema de arquivos padrão hello, você pode usar um caminho relativo ou um caminho absoluto.</span><span class="sxs-lookup"><span data-stu-id="b541f-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="b541f-222">Por exemplo, Olá *Hadoop-Examples.jar mapreduce* arquivo vem com clusters de HDInsight pode ser chamado tooby usando um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="b541f-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="b541f-223">nome de arquivo Hello <i>Hadoop-Examples.jar</i> em clusters de versões 2.1 e 1.6 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="b541f-224">Olá &lt;caminho&gt; é o nome de caminho HDFS de arquivo ou diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="b541f-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="b541f-225">Como os contêineres no Armazenamento do Azure são apenas um repositório de chave-valor, não há nenhum sistema de arquivos hierárquico verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="b541f-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="b541f-226">Um caractere "/" dentro de uma chave de blob é interpretado como um separador de diretório.</span><span class="sxs-lookup"><span data-stu-id="b541f-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="b541f-227">Por exemplo, o nome de blob Olá para *Hadoop-Examples.jar mapreduce* é:</span><span class="sxs-lookup"><span data-stu-id="b541f-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="b541f-228">Ao trabalhar com blobs fora do HDInsight, a maioria dos utilitários não reconhece o formato WASB hello e em vez disso, espera um formato de caminho básicas, como `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="b541f-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="b541f-229">Acessar blobs</span><span class="sxs-lookup"><span data-stu-id="b541f-229">Access blobs</span></span> 


### <span data-ttu-id="b541f-230"><a name="access-blobs-using-azure-powershell"></a> Usar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b541f-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="b541f-231">comandos de saudação nesta seção fornecem um exemplo básico de como usar o PowerShell tooaccess dados armazenados em blobs.</span><span class="sxs-lookup"><span data-stu-id="b541f-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="b541f-232">Para obter um exemplo mais completo que é personalizado para trabalhar com HDInsight, consulte Olá [ferramentas HDInsight](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="b541f-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="b541f-233">Use Olá comando toolist Olá relacionados ao blob cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="b541f-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Lista de cmdlets do PowerShell relacionados ao blob.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="b541f-235">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="b541f-235">Upload files</span></span>
<span data-ttu-id="b541f-236">Consulte [carregar dados tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="b541f-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="b541f-237">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="b541f-237">Download files</span></span>
<span data-ttu-id="b541f-238">Olá, script a seguir baixa uma pasta atual do toohello de blob de bloco.</span><span class="sxs-lookup"><span data-stu-id="b541f-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="b541f-239">Executando o script hello, antes de alterar pasta de tooa de diretório Olá onde você tem permissões de gravação.</span><span class="sxs-lookup"><span data-stu-id="b541f-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="b541f-240">Fornecer o nome do grupo de recursos de saudação e nome do cluster Olá, você pode usar o hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="b541f-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="b541f-241">Excluir arquivos</span><span class="sxs-lookup"><span data-stu-id="b541f-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="b541f-242">Listar arquivos</span><span class="sxs-lookup"><span data-stu-id="b541f-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="b541f-243">Executar consultas do Hive usando uma conta de armazenamento indefinida</span><span class="sxs-lookup"><span data-stu-id="b541f-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="b541f-244">Este exemplo mostra como toolist uma pasta da conta de armazenamento que não é definida durante a Olá o processo de criação.</span><span class="sxs-lookup"><span data-stu-id="b541f-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="b541f-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="b541f-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="b541f-246">Usar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b541f-246">Use Azure CLI</span></span>
<span data-ttu-id="b541f-247">Use Olá comandos toolist Olá relacionados ao blob de comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b541f-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="b541f-248">**Exemplo de como usar um arquivo de tooupload de CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="b541f-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="b541f-249">**Exemplo de como usar um arquivo de toodownload de CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="b541f-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="b541f-250">**Exemplo de como usar um arquivo de toodelete de CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="b541f-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="b541f-251">**Exemplo de como usar arquivos de toolist CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="b541f-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="b541f-252">Usar contas de armazenamento adicionais</span><span class="sxs-lookup"><span data-stu-id="b541f-252">Use additional storage accounts</span></span>

<span data-ttu-id="b541f-253">Ao criar um cluster HDInsight, você deve especificar conta de armazenamento do Azure Olá que deseja tooassociate com ele.</span><span class="sxs-lookup"><span data-stu-id="b541f-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="b541f-254">Além disso toothis conta de armazenamento, você pode adicionar contas de armazenamento adicional da saudação mesmo assinatura do Azure ou em diferentes assinaturas do Azure durante o processo de criação de saudação ou depois de um cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="b541f-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="b541f-255">Para obter instruções sobre como adicionar mais contas de armazenamento, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b541f-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="b541f-256">Não há suporte para usando uma conta de armazenamento adicional no cluster do HDInsight Olá um local diferente.</span><span class="sxs-lookup"><span data-stu-id="b541f-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b541f-257">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b541f-257">Next steps</span></span>
<span data-ttu-id="b541f-258">Neste artigo, você aprendeu como toouse HDFS compatível com o armazenamento do Azure com HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b541f-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="b541f-259">Isso permite que você toobuild escalonável e de longo prazo, arquivamento soluções de aquisição de dados e uso HDInsight toounlock Olá informações dentro de saudação armazenada estruturados e dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="b541f-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="b541f-260">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="b541f-260">For more information, see:</span></span>

* <span data-ttu-id="b541f-261">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b541f-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="b541f-262">Introdução ao Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b541f-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="b541f-263">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="b541f-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="b541f-264">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b541f-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="b541f-265">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b541f-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="b541f-266">[Usar assinaturas de acesso compartilhado do Azure Storage toorestrict acesso toodata com HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="b541f-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
