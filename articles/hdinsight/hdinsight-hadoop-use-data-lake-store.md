---
title: "aaaUse repositório Data Lake com Hadoop no HDInsight do Azure | Microsoft Docs"
description: "Saiba como os dados de tooquery do repositório Azure Data Lake e toostore resultados da análise."
keywords: "armazenamento de blobs, hdfs, dados estruturados, dados não estruturados, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="51af3-104">Usar o Data Lake Store com clusters Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="51af3-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="51af3-105">dados de tooanalyze no cluster HDInsight, você pode armazenar dados de saudação ou em [armazenamento do Azure](../storage/common/storage-introduction.md), [repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md), ou ambos.</span><span class="sxs-lookup"><span data-stu-id="51af3-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="51af3-106">Ambas as opções de armazenamento permitem que você exclua toosafely clusters de HDInsight que são usados para a computação sem perda de dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="51af3-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="51af3-107">Neste artigo, você aprenderá como o Data Lake Store funciona com clusters do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="51af3-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="51af3-108">toolearn como o armazenamento do Azure funciona com clusters de HDInsight, consulte [clusters de armazenamento do Azure Use com o Azure HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="51af3-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="51af3-109">Para saber mais sobre a criação de um cluster HDInsight, veja [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="51af3-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="51af3-110">O Data Lake Store é sempre acessado por meio de um canal seguro, portanto não há nenhum nome do esquema de sistema de arquivos `adls`.</span><span class="sxs-lookup"><span data-stu-id="51af3-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="51af3-111">Use sempre `adl`.</span><span class="sxs-lookup"><span data-stu-id="51af3-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="51af3-112">Disponibilidade para clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="51af3-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="51af3-113">Hadoop oferece suporte a uma noção saudação padrão do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="51af3-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="51af3-114">sistema de arquivos padrão Olá implica um esquema padrão e uma autoridade.</span><span class="sxs-lookup"><span data-stu-id="51af3-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="51af3-115">Ele também pode ser usado tooresolve os caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="51af3-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="51af3-116">Durante o processo de criação do cluster do HDInsight hello, você pode especificar um contêiner de blob no armazenamento do Azure como sistema de arquivos padrão hello, ou com HDInsight 3.5 e versões mais recentes, você pode selecionar armazenamento do Azure ou repositório Azure Data Lake como sistema de arquivos padrão Olá com um algumas exceções.</span><span class="sxs-lookup"><span data-stu-id="51af3-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="51af3-117">Os clusters HDInsight podem usar o Data Lake Store de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="51af3-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="51af3-118">Como o armazenamento padrão da saudação</span><span class="sxs-lookup"><span data-stu-id="51af3-118">As hello default storage</span></span>
* <span data-ttu-id="51af3-119">Como armazenamento adicional, com o Azure Storage Blob como o armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="51af3-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="51af3-120">A partir de agora, apenas algumas das Olá HDInsight cluster usando o repositório Data Lake como armazenamento padrão e as contas de armazenamento adicionais de suporte de tipos/versões:</span><span class="sxs-lookup"><span data-stu-id="51af3-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="51af3-121">Tipo de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="51af3-121">HDInsight cluster type</span></span> | <span data-ttu-id="51af3-122">Data Lake Store como armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="51af3-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="51af3-123">Data Lake Store como armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="51af3-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="51af3-124">Observações</span><span class="sxs-lookup"><span data-stu-id="51af3-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="51af3-125">HDInsight versão 3.6</span><span class="sxs-lookup"><span data-stu-id="51af3-125">HDInsight version 3.6</span></span> | <span data-ttu-id="51af3-126">Sim</span><span class="sxs-lookup"><span data-stu-id="51af3-126">Yes</span></span> | <span data-ttu-id="51af3-127">Sim</span><span class="sxs-lookup"><span data-stu-id="51af3-127">Yes</span></span> | |
| <span data-ttu-id="51af3-128">HDInsight versão 3.5</span><span class="sxs-lookup"><span data-stu-id="51af3-128">HDInsight version 3.5</span></span> | <span data-ttu-id="51af3-129">Sim</span><span class="sxs-lookup"><span data-stu-id="51af3-129">Yes</span></span> | <span data-ttu-id="51af3-130">Sim</span><span class="sxs-lookup"><span data-stu-id="51af3-130">Yes</span></span> | <span data-ttu-id="51af3-131">Com exceção de saudação do HBase</span><span class="sxs-lookup"><span data-stu-id="51af3-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="51af3-132">HDInsight versão 3.4</span><span class="sxs-lookup"><span data-stu-id="51af3-132">HDInsight version 3.4</span></span> | <span data-ttu-id="51af3-133">Não</span><span class="sxs-lookup"><span data-stu-id="51af3-133">No</span></span> | <span data-ttu-id="51af3-134">Sim</span><span class="sxs-lookup"><span data-stu-id="51af3-134">Yes</span></span> | |
| <span data-ttu-id="51af3-135">HDInsight versão 3.3</span><span class="sxs-lookup"><span data-stu-id="51af3-135">HDInsight version 3.3</span></span> | <span data-ttu-id="51af3-136">Não</span><span class="sxs-lookup"><span data-stu-id="51af3-136">No</span></span> | <span data-ttu-id="51af3-137">Não</span><span class="sxs-lookup"><span data-stu-id="51af3-137">No</span></span> | |
| <span data-ttu-id="51af3-138">HDInsight versão 3.2</span><span class="sxs-lookup"><span data-stu-id="51af3-138">HDInsight version 3.2</span></span> | <span data-ttu-id="51af3-139">Não</span><span class="sxs-lookup"><span data-stu-id="51af3-139">No</span></span> | <span data-ttu-id="51af3-140">Sim</span><span class="sxs-lookup"><span data-stu-id="51af3-140">Yes</span></span> | |
| <span data-ttu-id="51af3-141">HDInsight Premium (camada)</span><span class="sxs-lookup"><span data-stu-id="51af3-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="51af3-142">Não</span><span class="sxs-lookup"><span data-stu-id="51af3-142">No</span></span> | <span data-ttu-id="51af3-143">Não</span><span class="sxs-lookup"><span data-stu-id="51af3-143">No</span></span> | |
| <span data-ttu-id="51af3-144">Storm</span><span class="sxs-lookup"><span data-stu-id="51af3-144">Storm</span></span> | | |<span data-ttu-id="51af3-145">Você pode usar dados do repositório Data Lake toowrite de uma topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="51af3-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="51af3-146">Também é possível usar o Data Lake Store para dados de referência que, em seguida, podem ser lidos por uma topologia do Storm.</span><span class="sxs-lookup"><span data-stu-id="51af3-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="51af3-147">Usando o repositório Data Lake como uma conta de armazenamento adicional não afetam o desempenho ou tooread de capacidade de saudação ou gravar tooAzure armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="51af3-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="51af3-148">Usar o Data Lake Store como armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="51af3-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="51af3-149">Quando HDInsight é implantado com o repositório Data Lake como armazenamento padrão, os arquivos de relacionadas ao cluster de saudação são armazenados no repositório Data Lake em Olá local a seguir:</span><span class="sxs-lookup"><span data-stu-id="51af3-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="51af3-150">onde `<cluster_root_path>` é o nome de saudação de uma pasta que você criar no repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="51af3-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="51af3-151">Especificando um caminho raiz para cada cluster, você pode usar Olá a mesma conta de repositório Data Lake para mais de um cluster.</span><span class="sxs-lookup"><span data-stu-id="51af3-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="51af3-152">Portanto, você terá uma configuração em que:</span><span class="sxs-lookup"><span data-stu-id="51af3-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="51af3-153">Cluster1 pode usar o caminho de saudação`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="51af3-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="51af3-154">Cluster2 pode usar o caminho de saudação`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="51af3-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="51af3-155">Observe que ambos Olá use clusters Olá mesma conta do repositório Data Lake **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="51af3-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="51af3-156">Cada cluster tem acesso tooits possui o sistema de arquivos raiz no repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="51af3-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="51af3-157">Olá experiência de implantação do portal do Azure em particular solicitará que você toouse um nome de pasta, como **/clusters/\<clustername >** para caminho de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="51af3-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="51af3-158">toobe toouse capaz de um repositório Data Lake como armazenamento padrão, você deve conceder toohello de acesso principal do serviço Olá caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="51af3-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="51af3-159">raiz de conta do repositório Data Lake Hello.</span><span class="sxs-lookup"><span data-stu-id="51af3-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="51af3-160">Por exemplo: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="51af3-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="51af3-161">pasta de saudação para todas as pastas de cluster.</span><span class="sxs-lookup"><span data-stu-id="51af3-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="51af3-162">Por exemplo: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="51af3-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="51af3-163">pasta Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="51af3-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="51af3-164">Por exemplo: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="51af3-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="51af3-165">Para saber mais sobre como criar a entidade de segurança e conceder acesso, consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="51af3-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="51af3-166">Usar o Data Lake Store como armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="51af3-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="51af3-167">Você pode usar o repositório Data Lake como armazenamento adicional para o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="51af3-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="51af3-168">Nesses casos, armazenamento padrão da saudação cluster pode ser um Blob de armazenamento do Azure ou uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="51af3-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="51af3-169">Se você estiver executando trabalhos de HDInsight em relação aos dados Olá armazenados no repositório Data Lake como armazenamento adicional, você deve usar arquivos de toohello Olá caminho totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="51af3-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="51af3-170">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="51af3-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="51af3-171">Observe que não há nenhum **cluster_root_path** na URL de saudação agora.</span><span class="sxs-lookup"><span data-stu-id="51af3-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="51af3-172">Isso ocorre porque o repositório Data Lake não está um armazenamento padrão nesse caso você toodo só precisa fornecer Olá caminho toohello arquivos.</span><span class="sxs-lookup"><span data-stu-id="51af3-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="51af3-173">toobe toouse capaz de um repositório Data Lake como armazenamento adicional, você só precisa toogrant Olá acesso principal toohello caminhos de serviço de onde os arquivos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="51af3-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="51af3-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="51af3-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="51af3-175">Para saber mais sobre como criar a entidade de segurança e conceder acesso, consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="51af3-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="51af3-176">Usar mais de uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="51af3-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="51af3-177">Adicionar uma conta do repositório Data Lake como adicionais e adicionar mais de um repositório do Data Lake contas são realizadas, fornecendo permissão de cluster do HDInsight Olá em dados em uma ou mais contas de repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="51af3-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="51af3-178">Consulte [Configurar acesso ao Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="51af3-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="51af3-179">Configurar acesso ao Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="51af3-179">Configure Data Lake store access</span></span>

<span data-ttu-id="51af3-180">tooconfigure acesso ao repositório Data Lake do seu cluster HDInsight, você deve ter uma entidade de serviço do Azure Active directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="51af3-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="51af3-181">Somente um administrador do Azure AD pode criar uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="51af3-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="51af3-182">entidade de serviço Olá deve ser criada com um certificado.</span><span class="sxs-lookup"><span data-stu-id="51af3-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="51af3-183">Para obter mais informações, consulte [Configurar acesso ao Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) e [Criar entidade de serviço com certificado autoassinado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="51af3-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="51af3-184">Se você for repositório toouse Azure Data Lake como armazenamento adicional para o cluster HDInsight, é altamente recomendável que você faça isso durante a criação de cluster Olá conforme descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="51af3-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="51af3-185">Adicionar repositório Azure Data Lake como armazenamento adicional tooan cluster HDInsight existente é um processo complicado e sujeito a tooerrors.</span><span class="sxs-lookup"><span data-stu-id="51af3-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="51af3-186">Acessar arquivos do cluster Olá</span><span class="sxs-lookup"><span data-stu-id="51af3-186">Access files from hello cluster</span></span>

<span data-ttu-id="51af3-187">Há várias maneiras que você pode acessar arquivos Olá no repositório Data Lake de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="51af3-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="51af3-188">**Usando o nome totalmente qualificado da saudação**.</span><span class="sxs-lookup"><span data-stu-id="51af3-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="51af3-189">Com essa abordagem, você fornecer o arquivo de toohello de caminho completo de saudação que você deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="51af3-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="51af3-190">**Usando o formato de caminho reduzido Olá**.</span><span class="sxs-lookup"><span data-stu-id="51af3-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="51af3-191">Com essa abordagem, você deve substituir caminho Olá a raiz do cluster toohello com publicitário: / / /.</span><span class="sxs-lookup"><span data-stu-id="51af3-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="51af3-192">Portanto, o exemplo hello acima, você pode substituir `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` com `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="51af3-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="51af3-193">**Usando o caminho relativo Olá**.</span><span class="sxs-lookup"><span data-stu-id="51af3-193">**Using hello relative path**.</span></span> <span data-ttu-id="51af3-194">Com essa abordagem, você fornece apenas Olá relativo caminho toohello arquivo que você deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="51af3-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="51af3-195">Por exemplo, se Olá caminho completo toohello arquivo:</span><span class="sxs-lookup"><span data-stu-id="51af3-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="51af3-196">Você pode acessar Olá mesmo arquivo sample.log usando este caminho relativo, em vez disso.</span><span class="sxs-lookup"><span data-stu-id="51af3-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="51af3-197">Criar clusters de HDInsight com acessar o repositório de Lake tooData</span><span class="sxs-lookup"><span data-stu-id="51af3-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="51af3-198">Use Olá siga os links para obter instruções detalhadas de como toocreate clusters de HDInsight com acessar o repositório de Lake tooData.</span><span class="sxs-lookup"><span data-stu-id="51af3-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="51af3-199">Usando o Portal</span><span class="sxs-lookup"><span data-stu-id="51af3-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="51af3-200">Usando o PowerShell (com o Data Lake Store como o armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="51af3-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="51af3-201">Usando o PowerShell (com o Data Lake Store como o armazenamento adicional)</span><span class="sxs-lookup"><span data-stu-id="51af3-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="51af3-202">Usando modelos do Azure</span><span class="sxs-lookup"><span data-stu-id="51af3-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="51af3-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51af3-203">Next steps</span></span>
<span data-ttu-id="51af3-204">Neste artigo, você aprendeu como toouse repositório Azure Data Lake HDFS compatível com HDInsight.</span><span class="sxs-lookup"><span data-stu-id="51af3-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="51af3-205">Isso permite que você toobuild escalonável e de longo prazo, arquivamento soluções de aquisição de dados e uso HDInsight toounlock Olá informações dentro de saudação armazenada estruturados e dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="51af3-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="51af3-206">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="51af3-206">For more information, see:</span></span>

* <span data-ttu-id="51af3-207">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="51af3-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="51af3-208">Introdução ao Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="51af3-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="51af3-209">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="51af3-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="51af3-210">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="51af3-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="51af3-211">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="51af3-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="51af3-212">[Usar assinaturas de acesso compartilhado do Azure Storage toorestrict acesso toodata com HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="51af3-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
