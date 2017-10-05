---
title: Gerenciar clusters Hadoop baseados no Windows no HDInsight usando o Portal do Azure | Microsoft Docs
description: "Saiba como administrar o serviço do HDInsight. Crie um cluster HDInsight, abra o console interativo do JavaScript e abra o console de comando Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: f69fa4f838b22ccbb25186c08cac9744bb31c6d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-the-azure-portal"></a><span data-ttu-id="9f24c-104">Gerenciar clusters Hadoop baseados no Windows no HDInsight usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9f24c-104">Manage Windows-based Hadoop clusters in HDInsight by using the Azure portal</span></span>

<span data-ttu-id="9f24c-105">Ao usar o [Portal do Azure][azure-portal], você pode criar clusters Hadoop baseados no Windows no Azure HDInsight, alterar a senha de usuário do Hadoop e habilitar o RDP (Protocolo de Área de Trabalho Remota) para que você possa acessar o console de comando do Hadoop no cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-105">Using the [Azure portal][azure-portal], you can create Windows-based Hadoop clusters in Azure HDInsight, change Hadoop user password, and enable Remote Desktop Protocol (RDP) so you can access the Hadoop command console on the cluster.</span></span>

<span data-ttu-id="9f24c-106">As informações neste artigo aplicam-se apenas aos clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="9f24c-106">The information in this article only applies to Window-based HDInsight clusters.</span></span> <span data-ttu-id="9f24c-107">Para obter informações sobre como gerenciar clusters baseados no Linux, confira [Gerenciar clusters Hadoop no HDInsight usando o Portal do Azure](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-107">For information on managing Linux-based clusters, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-portal-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f24c-108">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="9f24c-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9f24c-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9f24c-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9f24c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9f24c-110">Prerequisites</span></span>

<span data-ttu-id="9f24c-111">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9f24c-111">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="9f24c-112">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-112">**An Azure subscription**.</span></span> <span data-ttu-id="9f24c-113">Consulte [Obter a avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9f24c-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9f24c-114">**Conta de armazenamento do Azure** - um cluster do HDInsight usa um contêiner de Armazenamento de Blob do Azure como o sistema de arquivos padrão.</span><span class="sxs-lookup"><span data-stu-id="9f24c-114">**Azure Storage account** - An HDInsight cluster uses an Azure Blob storage container as the default file system.</span></span> <span data-ttu-id="9f24c-115">Para obter mais informações sobre como o Armazenamento de Blob do Azure fornece uma experiência perfeita com os clusters HDInsight, consulte [Usar o Armazenamento de Blob do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-115">For more information about how Azure Blob storage provides a seamless experience with HDInsight clusters, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="9f24c-116">Para obter detalhes sobre como criar uma conta do Armazenamento do Azure, consulte [Como criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-116">For details on creating an Azure Storage account, see [How to Create a Storage Account](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="open-the-portal"></a><span data-ttu-id="9f24c-117">Abra o Portal</span><span class="sxs-lookup"><span data-stu-id="9f24c-117">Open the Portal</span></span>
1. <span data-ttu-id="9f24c-118">Entre em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9f24c-118">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f24c-119">Depois de abrir o portal, você poderá:</span><span class="sxs-lookup"><span data-stu-id="9f24c-119">After you open the portal, you can:</span></span>

   * <span data-ttu-id="9f24c-120">Clique em **Novo** no menu esquerdo para criar um novo cluster:</span><span class="sxs-lookup"><span data-stu-id="9f24c-120">Click **New** from the left menu to create a new cluster:</span></span>

       ![novo botão do cluster HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * <span data-ttu-id="9f24c-122">Clique em **Clusters HDInsight** no menu esquerdo.</span><span class="sxs-lookup"><span data-stu-id="9f24c-122">Click **HDInsight Clusters** from the left menu.</span></span>

       ![Botão do cluster HDInsight do Portal do Azure](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     <span data-ttu-id="9f24c-124">Se **HDInsight** não aparecer no menu esquerdo, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-124">If **HDInsight** doesn't appear in the left menu, click **Browse**.</span></span>

     ![Botão Procurar cluster do Portal do Azure](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a><span data-ttu-id="9f24c-126">Criar clusters</span><span class="sxs-lookup"><span data-stu-id="9f24c-126">Create clusters</span></span>
<span data-ttu-id="9f24c-127">Para obter as instruções de criação usando o Portal, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-127">For the creation instructions using the Portal, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="9f24c-128">O HDInsight trabalha com uma ampla variedade de componentes do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9f24c-128">HDInsight works with a wide range of Hadoop components.</span></span> <span data-ttu-id="9f24c-129">Para obter a lista dos componentes que foram verificados e com suporte, consulte [Qual versão do Hadoop está no HDInsight do Azure](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-129">For the list of the components that have been verified and supported, see [What version of Hadoop is in Azure HDInsight](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="9f24c-130">Você pode personalizar o HDInsight usando uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="9f24c-130">You can customize HDInsight by using one of the following options:</span></span>

* <span data-ttu-id="9f24c-131">Use a ação de Script para executar scripts personalizados que possam personalizar um cluster para alterar a configuração de cluster ou instalar componentes personalizados como Giraph ou Solr.</span><span class="sxs-lookup"><span data-stu-id="9f24c-131">Use Script Action to run custom scripts that can customize a cluster to either change cluster configuration or install custom components such as Giraph or Solr.</span></span> <span data-ttu-id="9f24c-132">Para obter mais informações, consulte [Personalizar cluster HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-132">For more information, see [Customize HDInsight cluster using Script Action](hdinsight-hadoop-customize-cluster.md).</span></span>
* <span data-ttu-id="9f24c-133">Use os parâmetros de personalização do cluster no SDK do .NET do HDInsight ou no PowerShell do Azure durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-133">Use the cluster customization parameters in the HDInsight .NET SDK or Azure PowerShell during cluster creation.</span></span> <span data-ttu-id="9f24c-134">Essas alterações de configuração são preservadas durante o tempo de vida do cluster e não são afetadas pelas novas imagens do nó do cluster que a plataforma do Azure refaz periodicamente para manutenção.</span><span class="sxs-lookup"><span data-stu-id="9f24c-134">These configuration changes are then preserved through the lifetime of the cluster and are not affected by cluster node reimages that Azure platform periodically performs for maintenance.</span></span> <span data-ttu-id="9f24c-135">Para mais informações sobre como usar os parâmetros de personalização do cluster, consulte [Criar clusters do HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-135">For more information on using the cluster customization parameters, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="9f24c-136">Alguns componentes nativos do Java, como Mahout e Cascading, podem ser executados no cluster como arquivos JAR.</span><span class="sxs-lookup"><span data-stu-id="9f24c-136">Some native Java components, like Mahout and Cascading, can be run on the cluster as JAR files.</span></span> <span data-ttu-id="9f24c-137">Esses arquivos JAR podem ser distribuídos para o armazenamento de Blob do Azure e enviados aos clusters HDInsight por meio de mecanismos de envio de trabalho do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9f24c-137">These JAR files can be distributed to Azure Blob storage, and submitted to HDInsight clusters through Hadoop job submission mechanisms.</span></span> <span data-ttu-id="9f24c-138">Para obter mais informações, consulte [Enviar trabalhos do Hadoop de forma programática](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-138">For more information, see [Submit Hadoop jobs programmatically](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

  > [!NOTE]
  > <span data-ttu-id="9f24c-139">Se você tiver problemas para implantar arquivos JAR nos clusters do HDInsight ou ao chamar arquivos JAR nesses clusters, entre em contato com o [Suporte da Microsoft](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="9f24c-139">If you have issues deploying JAR files to HDInsight clusters or calling JAR files on HDInsight clusters, contact [Microsoft Support](https://azure.microsoft.com/support/options/).</span></span>
  >
  > <span data-ttu-id="9f24c-140">O Cascading não tem suporte do HDInsight e não é qualificado para o Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f24c-140">Cascading is not supported by HDInsight, and is not eligible for Microsoft Support.</span></span> <span data-ttu-id="9f24c-141">Para obter as listas dos componentes suportados, confira [Novidades nas versões de cluster fornecidas pelo HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-141">For lists of supported components, see [What's new in the cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
  >
  >

<span data-ttu-id="9f24c-142">Não há suporte para a instalação de software personalizado no cluster usando uma conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="9f24c-142">Installation of custom software on the cluster by using Remote Desktop Connection is not supported.</span></span> <span data-ttu-id="9f24c-143">Evite armazenar arquivos nas unidades de nó de cabeçalho, pois eles serão perdidos se você precisar recriar os clusters.</span><span class="sxs-lookup"><span data-stu-id="9f24c-143">You should avoid storing any files on the drives of the head node, as they will be lost if you need to re-create the clusters.</span></span> <span data-ttu-id="9f24c-144">É recomendável armazenar os arquivos no armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-144">We recommend storing files on Azure Blob storage.</span></span> <span data-ttu-id="9f24c-145">O armazenamento de Blob é persistente.</span><span class="sxs-lookup"><span data-stu-id="9f24c-145">Blob storage is persistent.</span></span>

## <a name="list-and-show-clusters"></a><span data-ttu-id="9f24c-146">Listar e mostrar clusters</span><span class="sxs-lookup"><span data-stu-id="9f24c-146">List and show clusters</span></span>
1. <span data-ttu-id="9f24c-147">Entre em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9f24c-147">Sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f24c-148">Clique em **Clusters HDInsight** no menu esquerdo.</span><span class="sxs-lookup"><span data-stu-id="9f24c-148">Click **HDInsight Clusters** from the left menu.</span></span>
3. <span data-ttu-id="9f24c-149">Clique no nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-149">Click the cluster name.</span></span> <span data-ttu-id="9f24c-150">Se a lista de clusters for longa, você poderá usar o filtro na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="9f24c-150">If the cluster list is long, you can use filter on the top of the page.</span></span>
4. <span data-ttu-id="9f24c-151">Clique duas vezes em um cluster da lista para exibir os detalhes.</span><span class="sxs-lookup"><span data-stu-id="9f24c-151">Double-click a cluster from the list to show the details.</span></span>

    <span data-ttu-id="9f24c-152">**Menu e fundamentos**:</span><span class="sxs-lookup"><span data-stu-id="9f24c-152">**Menu and essentials**:</span></span>

    ![Fundamentos do cluster HDInsight do portal do Azure](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * <span data-ttu-id="9f24c-154">Para personalizar o menu, clique com o botão direito do mouse em qualquer parte do menu e, então, clique em **Personalizar**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-154">To customize the menu, right-click anywhere on the menu, and then click **Customize**.</span></span>
   * <span data-ttu-id="9f24c-155">**Configurações** e **Todas as Configurações**: exibem a folha **Configurações** do cluster, que permite acessar informações de configuração detalhadas do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-155">**Settings** and **All Settings**: Displays the **Settings** blade for the cluster, which allows you to access detailed configuration information for the cluster.</span></span>
   * <span data-ttu-id="9f24c-156">**Painel**, **Painel do Cluster** e **URL: são maneiras de acessar o painel do cluster, que é o Ambari Web para clusters baseados em Linux. -**Secure Shell**: mostra as instruções para se conectar ao cluster usando uma conexão Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="9f24c-156">**Dashboard**, **Cluster Dashboard** and **URL: These are all ways to access the cluster dashboard, which is Ambari Web for Linux-based clusters. -**Secure Shell**: Shows the instructions to connect to the cluster using Secure Shell (SSH) connection.</span></span>
   * <span data-ttu-id="9f24c-157">**Cluster em Escala**: permite alterar o número de nós de trabalho deste cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-157">**Scale Cluster**: Allows you to change the number of worker nodes for this cluster.</span></span>
   * <span data-ttu-id="9f24c-158">**Excluir**: exclui o cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-158">**Delete**: Deletes the cluster.</span></span>
   * <span data-ttu-id="9f24c-159">**Início Rápido**: exibe informações que o ajudarão a começar a usar o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-159">**Quickstart**: Displays information that will help you get started using HDInsight.</span></span>
   * <span data-ttu-id="9f24c-160">**Usuários: permite definir permissões para o *gerenciamento do portal* deste cluster para outros usuários em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-160">**Users: Allows you to set permissions for *portal management* of this cluster for other users on your Azure subscription.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="9f24c-161">Isso afeta *apenas* o acesso e as permissões para esse cluster no Portal do Azure e não afeta quem pode se conectar ao cluster HDInsight ou enviar trabalhos a ele.</span><span class="sxs-lookup"><span data-stu-id="9f24c-161">This *only* affects access and permissions to this cluster in the Azure portal, and has no effect on who can connect to or submit jobs to the HDInsight cluster.</span></span>
     >
     >
   * <span data-ttu-id="9f24c-162">**Marcas**: as marcas permitem estabelecer pares de chave/valor para definir uma taxonomia personalizada dos serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="9f24c-162">**Tags**: Tags allow you to set key/value pairs to define a custom taxonomy of your cloud services.</span></span> <span data-ttu-id="9f24c-163">Por exemplo, você pode criar uma chave chamada **projeto**e usar um valor comum para todos os serviços associados a um projeto específico.</span><span class="sxs-lookup"><span data-stu-id="9f24c-163">For example, you may create a key named **project**, and then use a common value for all services associated with a specific project.</span></span>
   * <span data-ttu-id="9f24c-164">**Ambari Views**: links para o Ambari Web.</span><span class="sxs-lookup"><span data-stu-id="9f24c-164">**Ambari Views**: Links to Ambari Web.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="9f24c-165">Para gerenciar os serviços fornecidos pelo cluster HDInsight, você deve usar o Ambari Web ou a API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="9f24c-165">To manage the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="9f24c-166">Para saber mais sobre como usar o Ambari, consulte [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-166">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
     >
     >

     <span data-ttu-id="9f24c-167">**Uso**:</span><span class="sxs-lookup"><span data-stu-id="9f24c-167">**Usage**:</span></span>

     ![Uso do cluster HDInsight do Portal do Azure](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. <span data-ttu-id="9f24c-169">Clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-169">Click **Settings**.</span></span>

    ![Uso do cluster HDInsight do Portal do Azure](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * <span data-ttu-id="9f24c-171">**Propriedades**: exiba as propriedades do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-171">**Properties**: View the cluster properties.</span></span>
   * <span data-ttu-id="9f24c-172">**Identidade do AAD do Cluster**:</span><span class="sxs-lookup"><span data-stu-id="9f24c-172">**Cluster AAD Identity**:</span></span>
   * <span data-ttu-id="9f24c-173">**Chaves de Armazenamento do Azure**: exiba a conta de armazenamento padrão e a chave dela.</span><span class="sxs-lookup"><span data-stu-id="9f24c-173">**Azure Storage Keys**: View the default storage account and its key.</span></span> <span data-ttu-id="9f24c-174">A conta de armazenamento é configurada durante o processo de criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-174">The storage account is configuration during the cluster creation process.</span></span>
   * <span data-ttu-id="9f24c-175">**Logon do Cluster**: altere o nome de usuário e a senha do HTTP de cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-175">**Cluster Login**: Change the cluster HTTP user name and password.</span></span>
   * <span data-ttu-id="9f24c-176">**Metastores Externos**: exiba os Hive e Oozie metastores.</span><span class="sxs-lookup"><span data-stu-id="9f24c-176">**External Metastores**: View the Hive and Oozie metastores.</span></span> <span data-ttu-id="9f24c-177">Os metastores só podem ser configurados durante o processo de criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-177">The metastores can only be configured during the cluster creation process.</span></span>
   * <span data-ttu-id="9f24c-178">**Dimensionar o Cluster**: aumente e diminua o número de nós de trabalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-178">**Scale Cluster**: Increase and decrease the number of cluster worker nodes.</span></span>
   * <span data-ttu-id="9f24c-179">**Área de Trabalho Remota**: habilite e desabilite o acesso da área de trabalho remota (RDP) e configure o nome de usuário da RDP.</span><span class="sxs-lookup"><span data-stu-id="9f24c-179">**Remote Desktop**: Enable and disable remote desktop (RDP) access, and configure the RDP username.</span></span>  <span data-ttu-id="9f24c-180">O nome de usuário da RDP deve ser diferente do nome de usuário de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9f24c-180">The RDP user name must be different from the HTTP user name.</span></span>
   * <span data-ttu-id="9f24c-181">**Parceiro de Registro**:</span><span class="sxs-lookup"><span data-stu-id="9f24c-181">**Partner of Record**:</span></span>

     > [!NOTE]
     > <span data-ttu-id="9f24c-182">Esta é uma lista genérica de configurações disponíveis; nem todas elas estarão presentes para todos os tipos de cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-182">This is a generic list of available settings; not all of them will be present for all cluster types.</span></span>
     >
     >
6. <span data-ttu-id="9f24c-183">Clique em **Propriedades**:</span><span class="sxs-lookup"><span data-stu-id="9f24c-183">Click **Properties**:</span></span>

    <span data-ttu-id="9f24c-184">A seção das propriedades lista o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9f24c-184">The properties section lists the following:</span></span>

   * <span data-ttu-id="9f24c-185">**Nome do host**: nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-185">**Hostname**: Cluster name.</span></span>
   * <span data-ttu-id="9f24c-186">**URL do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-186">**Cluster URL**.</span></span>
   * <span data-ttu-id="9f24c-187">**Status**: incluindo Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span><span class="sxs-lookup"><span data-stu-id="9f24c-187">**Status**: Include Aborted, Accepted, ClusterStorageProvisioned, AzureVMConfiguration, HDInsightConfiguration, Operational, Running, Error, Deleting, Deleted, Timedout, DeleteQueued, DeleteTimedout, DeleteError, PatchQueued, CertRolloverQueued, ResizeQueued, ClusterCustomization</span></span>
   * <span data-ttu-id="9f24c-188">**Região**: local do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-188">**Region**: Azure location.</span></span> <span data-ttu-id="9f24c-189">Para ter acesso à lista de locais do Azure com suporte, consulte a caixa de listagem suspensa **Região** em [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9f24c-189">For a list of supported Azure locations, see the **Region** dropdown list box on [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>
   * <span data-ttu-id="9f24c-190">**Dados criados**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-190">**Data created**.</span></span>
   * <span data-ttu-id="9f24c-191">**Sistema operacional**: **Windows** ou **Linux**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-191">**Operating system**: Either **Windows** or **Linux**.</span></span>
   * <span data-ttu-id="9f24c-192">**Tipo**: Hadoop, HBase, Storm, Spark.</span><span class="sxs-lookup"><span data-stu-id="9f24c-192">**Type**: Hadoop, HBase, Storm, Spark.</span></span>
   * <span data-ttu-id="9f24c-193">**Versão**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-193">**Version**.</span></span> <span data-ttu-id="9f24c-194">Consulte [versões do HDInsight](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="9f24c-194">See [HDInsight versions](hdinsight-component-versioning.md)</span></span>
   * <span data-ttu-id="9f24c-195">**Assinatura**: nome da assinatura.</span><span class="sxs-lookup"><span data-stu-id="9f24c-195">**Subscription**: Subscription name.</span></span>
   * <span data-ttu-id="9f24c-196"><seg>
  **ID da assinatura**.</seg></span><span class="sxs-lookup"><span data-stu-id="9f24c-196">**Subscription ID**.</span></span>
   * <span data-ttu-id="9f24c-197">**Fonte de dados primária**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-197">**Primary data source**.</span></span> <span data-ttu-id="9f24c-198">A conta de armazenamento de Blob do Azure usada como o sistema de arquivos Hadoop padrão.</span><span class="sxs-lookup"><span data-stu-id="9f24c-198">The Azure Blob storage account used as the default Hadoop file system.</span></span>
   * <span data-ttu-id="9f24c-199">**Faixa de preço dos nós de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-199">**Worker nodes pricing tier**.</span></span>
   * <span data-ttu-id="9f24c-200">**Faixa de preço do nó de cabeça**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-200">**Head node pricing tier**.</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="9f24c-201">Excluir clusters</span><span class="sxs-lookup"><span data-stu-id="9f24c-201">Delete clusters</span></span>
<span data-ttu-id="9f24c-202">Excluir um cluster não excluirá a conta de armazenamento padrão, nem nenhuma conta de armazenamento vinculada.</span><span class="sxs-lookup"><span data-stu-id="9f24c-202">Delete a cluster will not delete the default storage account or any linked storage accounts.</span></span> <span data-ttu-id="9f24c-203">Você pode recriar o cluster usando as mesmas contas de armazenamento e as mesmas metastores.</span><span class="sxs-lookup"><span data-stu-id="9f24c-203">You can re-create the cluster by using the same storage accounts and the same metastores.</span></span>

1. <span data-ttu-id="9f24c-204">Conecte-se no [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f24c-204">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="9f24c-205">Clique em **Procurar Tudo** no menu esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-205">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="9f24c-206">Clique em **Excluir** no menu superior e siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="9f24c-206">Click **Delete** from the top menu, and then follow the instructions.</span></span>

<span data-ttu-id="9f24c-207">Consulte também [Pausar/desligar clusters](#pauseshut-down-clusters).</span><span class="sxs-lookup"><span data-stu-id="9f24c-207">See also [Pause/shut down clusters](#pauseshut-down-clusters).</span></span>

## <a name="scale-clusters"></a><span data-ttu-id="9f24c-208">Dimensionar clusters</span><span class="sxs-lookup"><span data-stu-id="9f24c-208">Scale clusters</span></span>
<span data-ttu-id="9f24c-209">O recurso de dimensionamento de clusters permite que você altere o número de nós de trabalhador usados por um cluster em execução no Azure HDInsight sem precisar recriar o cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-209">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="9f24c-210">Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="9f24c-210">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="9f24c-211">Se não tiver certeza quanto à versão de seu cluster, você poderá verificar a página Propriedades.</span><span class="sxs-lookup"><span data-stu-id="9f24c-211">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="9f24c-212">Confira [Listar e mostrar clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="9f24c-212">See [List and show clusters](#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="9f24c-213">O impacto da alteração do número de nós de dados em cada tipo de cluster com suporte do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9f24c-213">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="9f24c-214">O Hadoop</span><span class="sxs-lookup"><span data-stu-id="9f24c-214">Hadoop</span></span>

    <span data-ttu-id="9f24c-215">Você pode aumentar continuamente o número de nós de trabalhador em um cluster Hadoop em execução sem afetar os trabalhos pendentes ou em execução.</span><span class="sxs-lookup"><span data-stu-id="9f24c-215">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="9f24c-216">Novos trabalhos também podem ser enviados enquanto a operação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="9f24c-216">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="9f24c-217">Falhas em uma operação de dimensionamento são normalmente manipuladas para que o cluster sempre seja deixado em um estado funcional.</span><span class="sxs-lookup"><span data-stu-id="9f24c-217">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="9f24c-218">Quando um cluster Hadoop é reduzido verticalmente pela diminuição do número de nós de dados, alguns dos serviços no cluster são reiniciados.</span><span class="sxs-lookup"><span data-stu-id="9f24c-218">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="9f24c-219">Isso faz com que todos os trabalhos em execução e pendentes falhem após a conclusão da operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9f24c-219">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="9f24c-220">Você pode, no entanto, reenviar os trabalhos quando a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="9f24c-220">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="9f24c-221">HBase</span><span class="sxs-lookup"><span data-stu-id="9f24c-221">HBase</span></span>

    <span data-ttu-id="9f24c-222">Você pode adicionar ou remover diretamente nós do cluster HBase enquanto ele é executado.</span><span class="sxs-lookup"><span data-stu-id="9f24c-222">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="9f24c-223">Servidores Regionais são equilibrados automaticamente em alguns minutos após o término da operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="9f24c-223">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="9f24c-224">No entanto, você pode equilibrar manualmente os servidores regionais fazendo logon no nó de cabeçalho do cluster e executando os seguintes comandos em uma janela de prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="9f24c-224">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    <span data-ttu-id="9f24c-225">Para obter mais informações sobre como usar o shell do HBase, confira []</span><span class="sxs-lookup"><span data-stu-id="9f24c-225">For more information on using the HBase shell, see []</span></span>
* <span data-ttu-id="9f24c-226">Storm</span><span class="sxs-lookup"><span data-stu-id="9f24c-226">Storm</span></span>

    <span data-ttu-id="9f24c-227">Você pode adicionar ou remover nós de dados continuamente para seu cluster Strom enquanto ele é executado.</span><span class="sxs-lookup"><span data-stu-id="9f24c-227">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="9f24c-228">Mas, após a conclusão bem-sucedida da operação de dimensionamento, você precisará redistribuir a topologia.</span><span class="sxs-lookup"><span data-stu-id="9f24c-228">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="9f24c-229">A redistribuição pode ser feita de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="9f24c-229">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="9f24c-230">Interface da Web Storm</span><span class="sxs-lookup"><span data-stu-id="9f24c-230">Storm web UI</span></span>
  * <span data-ttu-id="9f24c-231">Ferramenta CLI (interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="9f24c-231">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="9f24c-232">Consulte a [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9f24c-232">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="9f24c-233">A IU da Web do Storm está disponível no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9f24c-233">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight storm dimensionar novo balanceamento](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    <span data-ttu-id="9f24c-235">Aqui está um exemplo de como usar o comando CLI para reequilibrar a topologia do Storm:</span><span class="sxs-lookup"><span data-stu-id="9f24c-235">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="9f24c-236">**Para dimensionar clusters**</span><span class="sxs-lookup"><span data-stu-id="9f24c-236">**To scale clusters**</span></span>

1. <span data-ttu-id="9f24c-237">Conecte-se no [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f24c-237">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="9f24c-238">Clique em **Procurar Tudo** no menu esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-238">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="9f24c-239">Clique em **Configurações** no menu superior e clique em **Dimensionar o Cluster**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-239">Click **Settings** from the top menu, and then click **Scale Cluster**.</span></span>
4. <span data-ttu-id="9f24c-240">Insira o **Número de Nós de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-240">Enter **Number of Worker nodes**.</span></span> <span data-ttu-id="9f24c-241">O limite no número de nós do cluster varia entre as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-241">The limit on the number of cluster node varies among Azure subscriptions.</span></span> <span data-ttu-id="9f24c-242">Contate o suporte de cobrança para aumentar o limite.</span><span class="sxs-lookup"><span data-stu-id="9f24c-242">You can contact billing support to increase the limit.</span></span>  <span data-ttu-id="9f24c-243">As informações de custo refletirão as alterações feitas no número de nós.</span><span class="sxs-lookup"><span data-stu-id="9f24c-243">The cost information will reflect the changes you have made to the number of nodes.</span></span>

    ![HDInsight Hadoop HBase Storm Spark scale](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a><span data-ttu-id="9f24c-245">Pausar/desligar clusters</span><span class="sxs-lookup"><span data-stu-id="9f24c-245">Pause/shut down clusters</span></span>
<span data-ttu-id="9f24c-246">A maioria dos trabalhos do Hadoop é composta por trabalhos em lotes que só são executados ocasionalmente.</span><span class="sxs-lookup"><span data-stu-id="9f24c-246">Most of Hadoop jobs are batch jobs that are only ran occasionally.</span></span> <span data-ttu-id="9f24c-247">Para a maioria dos clusters do Hadoop, há grandes períodos de tempo em que o cluster não está sendo usado para processamento.</span><span class="sxs-lookup"><span data-stu-id="9f24c-247">For most Hadoop clusters, there are large periods of time that the cluster is not being used for processing.</span></span> <span data-ttu-id="9f24c-248">Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso.</span><span class="sxs-lookup"><span data-stu-id="9f24c-248">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span>
<span data-ttu-id="9f24c-249">Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso.</span><span class="sxs-lookup"><span data-stu-id="9f24c-249">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="9f24c-250">Como os encargos para o cluster são muitas vezes maiores do que os encargos para armazenamento, faz sentido, do ponto de vista econômico, excluir os clusters quando não estiverem em uso.</span><span class="sxs-lookup"><span data-stu-id="9f24c-250">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span>

<span data-ttu-id="9f24c-251">Há várias maneiras de programar o processo:</span><span class="sxs-lookup"><span data-stu-id="9f24c-251">There are many ways you can program the process:</span></span>

* <span data-ttu-id="9f24c-252">Use o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9f24c-252">User Azure Data Factory.</span></span> <span data-ttu-id="9f24c-253">Consulte [Serviços Vinculados ao Azure HDInsight](../data-factory/data-factory-compute-linked-services.md) e [Transformar e analisar usando o Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) para saber mais sobre os serviços sob demanda e autodefinidos vinculados ao HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-253">See [Azure HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md) and [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md) for on-demand and self-defined HDInsight linked services.</span></span>
* <span data-ttu-id="9f24c-254">Use o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f24c-254">Use Azure PowerShell.</span></span>  <span data-ttu-id="9f24c-255">Consulte [Analisar dados de atraso de voo](hdinsight-analyze-flight-delay-data.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-255">See [Analyze flight delay data](hdinsight-analyze-flight-delay-data.md).</span></span>
* <span data-ttu-id="9f24c-256">Use a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-256">Use Azure CLI.</span></span> <span data-ttu-id="9f24c-257">Consulte [Gerenciar clusters HDInsight usando a CLI do Azure](hdinsight-administer-use-command-line.md)</span><span class="sxs-lookup"><span data-stu-id="9f24c-257">See [Manage HDInsight clusters using Azure CLI](hdinsight-administer-use-command-line.md).</span></span>
* <span data-ttu-id="9f24c-258">Use o SDK .NET do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-258">Use HDInsight .NET SDK.</span></span> <span data-ttu-id="9f24c-259">Consulte [Enviar trabalhos do Hadoop](hdinsight-submit-hadoop-jobs-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-259">See [Submit Hadoop jobs](hdinsight-submit-hadoop-jobs-programmatically.md).</span></span>

<span data-ttu-id="9f24c-260">Para saber mais sobre preços, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9f24c-260">For the pricing information, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span> <span data-ttu-id="9f24c-261">Para excluir um cluster do Portal, veja [Excluir clusters](#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="9f24c-261">To delete a cluster from the Portal, see [Delete clusters](#delete-clusters)</span></span>

## <a name="change-cluster-username"></a><span data-ttu-id="9f24c-262">Alterar nome de usuário do cluster</span><span class="sxs-lookup"><span data-stu-id="9f24c-262">Change cluster username</span></span>
<span data-ttu-id="9f24c-263">Um cluster HDInsight pode ter duas contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="9f24c-263">An HDInsight cluster can have two user accounts.</span></span> <span data-ttu-id="9f24c-264">A conta de usuário do cluster HDInsight é criada durante o processo de criação.</span><span class="sxs-lookup"><span data-stu-id="9f24c-264">The HDInsight cluster user account is created during the creation process.</span></span> <span data-ttu-id="9f24c-265">Você também pode criar uma conta de usuário RDP para acessar o cluster via RDP.</span><span class="sxs-lookup"><span data-stu-id="9f24c-265">You can also create an RDP user account for accessing the cluster via RDP.</span></span> <span data-ttu-id="9f24c-266">Consulte [Habilitar área de trabalho remota](#connect-to-hdinsight-clusters-by-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="9f24c-266">See [Enable remote desktop](#connect-to-hdinsight-clusters-by-using-rdp).</span></span>

<span data-ttu-id="9f24c-267">**Para alterar o nome de usuário e a senha do cluster HDInsight**</span><span class="sxs-lookup"><span data-stu-id="9f24c-267">**To change the HDInsight cluster user name and password**</span></span>

1. <span data-ttu-id="9f24c-268">Conecte-se no [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f24c-268">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="9f24c-269">Clique em **Procurar Tudo** no menu esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-269">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="9f24c-270">Clique em **Configurações** no menu superior e clique em **Logon do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-270">Click **Settings** from the top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="9f24c-271">Se **Logon do cluster** tiver sido habilitado, você deverá clicar em **Desabilitar** e clicar em **Habilitar** antes de poder alterar o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="9f24c-271">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span></span>
5. <span data-ttu-id="9f24c-272">Altere o **Nome de Logon do Cluster** e/ou a **Senha de Logon do Cluster** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-272">Change the **Cluster Login Name** and/or the **Cluster Login Password**, and then click **Save**.</span></span>

    ![HDInsight change cluster user username password http user](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a><span data-ttu-id="9f24c-274">Conceder/revogar acesso</span><span class="sxs-lookup"><span data-stu-id="9f24c-274">Grant/revoke access</span></span>
<span data-ttu-id="9f24c-275">Os clusters HDInsight têm os seguintes serviços Web HTTP (todos esses serviços têm pontos de extremidade RESTful):</span><span class="sxs-lookup"><span data-stu-id="9f24c-275">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="9f24c-276">ODBC</span><span class="sxs-lookup"><span data-stu-id="9f24c-276">ODBC</span></span>
* <span data-ttu-id="9f24c-277">JDBC</span><span class="sxs-lookup"><span data-stu-id="9f24c-277">JDBC</span></span>
* <span data-ttu-id="9f24c-278">Ambari</span><span class="sxs-lookup"><span data-stu-id="9f24c-278">Ambari</span></span>
* <span data-ttu-id="9f24c-279">Oozie</span><span class="sxs-lookup"><span data-stu-id="9f24c-279">Oozie</span></span>
* <span data-ttu-id="9f24c-280">Templeton</span><span class="sxs-lookup"><span data-stu-id="9f24c-280">Templeton</span></span>

<span data-ttu-id="9f24c-281">Por padrão, esses serviços são concedidos para acesso.</span><span class="sxs-lookup"><span data-stu-id="9f24c-281">By default, these services are granted for access.</span></span> <span data-ttu-id="9f24c-282">Você pode revogar/conceder o acesso no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-282">You can revoke/grant the access from the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9f24c-283">Ao conceder/revogar o acesso, você redefinirá o nome de usuário de cluster e a senha.</span><span class="sxs-lookup"><span data-stu-id="9f24c-283">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="9f24c-284">**Para conceder/revogar acesso aos serviços Web HTTP**</span><span class="sxs-lookup"><span data-stu-id="9f24c-284">**To grant/revoke HTTP web services access**</span></span>

1. <span data-ttu-id="9f24c-285">Conecte-se no [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f24c-285">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="9f24c-286">Clique em **Procurar Tudo** no menu esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-286">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="9f24c-287">Clique em **Configurações** no menu superior e clique em **Logon do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-287">Click **Settings** from the top menu, and then click **Cluster Login**.</span></span>
4. <span data-ttu-id="9f24c-288">Se **Logon do cluster** tiver sido habilitado, você deverá clicar em **Desabilitar** e clicar em **Habilitar** antes de poder alterar o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="9f24c-288">If **Cluster login** has been enabled, you must click **Disable**, and then click **Enable** before you can change the username and password..</span></span>
5. <span data-ttu-id="9f24c-289">Para **Nome de Usuário de Logon no Cluster** e **Senha de Logon no Cluster**, insira o novo nome de usuário e a senha (respectivamente) para o cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-289">For **Cluster Login Username** and **Cluster Login Password**, enter the new user name and password (respectively) for the cluster.</span></span>
6. <span data-ttu-id="9f24c-290">Clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-290">Click **SAVE**.</span></span>

    ![HDInsight grand remove http web service access](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-the-default-storage-account"></a><span data-ttu-id="9f24c-292">Encontrar a conta de armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="9f24c-292">Find the default storage account</span></span>
<span data-ttu-id="9f24c-293">Cada cluster HDInsight tem uma conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="9f24c-293">Each HDInsight cluster has a default storage account.</span></span> <span data-ttu-id="9f24c-294">A conta de armazenamento padrão e as chaves para um cluster são exibidos em **Configurações**/**Propriedades**/**Chaves de Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-294">The default storage account and its keys for a cluster appears under **Settings**/**Properties**/**Azure Storage Keys**.</span></span> <span data-ttu-id="9f24c-295">Consulte [Listar e mostrar clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="9f24c-295">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="find-the-resource-group"></a><span data-ttu-id="9f24c-296">Encontrar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9f24c-296">Find the resource group</span></span>
<span data-ttu-id="9f24c-297">No modo Azure Resource Manager, cada cluster HDInsight é criado com um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-297">In the Azure Resource Manager mode, each HDInsight cluster is created with an Azure resource group.</span></span> <span data-ttu-id="9f24c-298">O grupo de recursos do Azure ao qual um cluster pertence aparece em:</span><span class="sxs-lookup"><span data-stu-id="9f24c-298">The Azure resource group that a cluster belongs to appears in:</span></span>

* <span data-ttu-id="9f24c-299">A lista de clusters tem uma coluna **Grupo de Recursos** .</span><span class="sxs-lookup"><span data-stu-id="9f24c-299">The cluster list has a **Resource Group** column.</span></span>
* <span data-ttu-id="9f24c-300">Bloco **Fundamentos** do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-300">Cluster **Essential** tile.</span></span>  

<span data-ttu-id="9f24c-301">Consulte [Listar e mostrar clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="9f24c-301">See [List and show clusters](#list-and-show-clusters).</span></span>

## <a name="open-hdinsight-query-console"></a><span data-ttu-id="9f24c-302">Abrir o console de Consulta do HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f24c-302">Open HDInsight Query console</span></span>
<span data-ttu-id="9f24c-303">O console de Consulta do HDInsight inclui os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="9f24c-303">The HDInsight Query console includes the following features:</span></span>

* <span data-ttu-id="9f24c-304">**Editor Hive**: uma interface GUI da Web para enviar trabalhos do Hive.</span><span class="sxs-lookup"><span data-stu-id="9f24c-304">**Hive Editor**: A GUI web interface for submitting Hive jobs.</span></span>  <span data-ttu-id="9f24c-305">Consulte [Executar consultas do Hive usando o Console de Consulta](hdinsight-hadoop-use-hive-query-console.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-305">See [Run Hive queries using the Query Console](hdinsight-hadoop-use-hive-query-console.md).</span></span>

    ![Editor de hive do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* <span data-ttu-id="9f24c-307">**Histórico de trabalhos**: monitore trabalhos do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9f24c-307">**Job history**: Monitor Hadoop jobs.</span></span>  

    ![histórico de trabalhos do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    <span data-ttu-id="9f24c-309">Clique em **Nome da Consulta** para mostrar os detalhes, incluindo propriedades do trabalho, **Consulta de Trabalho** e **Saída do Trabalho.</span><span class="sxs-lookup"><span data-stu-id="9f24c-309">Click **Query Name** to show the details including Job properties, **Job Query**, and **Job Output.</span></span> <span data-ttu-id="9f24c-310">Você também pode baixar a consulta e a saída para sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9f24c-310">You can also download both the query and the output to your workstation.</span></span>
* <span data-ttu-id="9f24c-311">**Navegador de Arquivos**: procure a conta de armazenamento padrão e as contas de armazenamento vinculadas.</span><span class="sxs-lookup"><span data-stu-id="9f24c-311">**File Browser**: Browse the default storage account and the linked storage accounts.</span></span>

    ![Pesquisa do navegador de arquivos do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    <span data-ttu-id="9f24c-313">Na captura de tela, o tipo **<Account>** indica que o item é uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f24c-313">On the screenshot, the **<Account>** type indicates the item is an Azure storage account.</span></span>  <span data-ttu-id="9f24c-314">Clique no nome da conta para procurar arquivos.</span><span class="sxs-lookup"><span data-stu-id="9f24c-314">Click the account name to browse the files.</span></span>
* <span data-ttu-id="9f24c-315">**IU do Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-315">**Hadoop UI**.</span></span>

    ![Interface do usuário do Hadoop do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    <span data-ttu-id="9f24c-317">Na **IU do Hadoop*, você pode procurar arquivos e verificar logs.</span><span class="sxs-lookup"><span data-stu-id="9f24c-317">From **Hadoop UI*, you can browse files, and check logs.</span></span>
* <span data-ttu-id="9f24c-318">**IU do Yarn**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-318">**Yarn UI**.</span></span>

    ![Interface do usuário do YARN do portal do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a><span data-ttu-id="9f24c-320">Execute consultas Hive</span><span class="sxs-lookup"><span data-stu-id="9f24c-320">Run Hive queries</span></span>
<span data-ttu-id="9f24c-321">Para executar trabalhos do Hive no Portal, clique em **Editor do Hive** no console da Consulta do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-321">To ran Hive jobs from the Portal, click **Hive Editor** in the HDInsight Query console.</span></span> <span data-ttu-id="9f24c-322">Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="9f24c-322">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-jobs"></a><span data-ttu-id="9f24c-323">Monitorar trabalhos</span><span class="sxs-lookup"><span data-stu-id="9f24c-323">Monitor jobs</span></span>
<span data-ttu-id="9f24c-324">Para monitorar trabalhos no Portal, clique em **Histórico de Trabalhos** no console da Consulta do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-324">To monitor jobs from the Portal, click **Job History** in the HDInsight Query console.</span></span> <span data-ttu-id="9f24c-325">Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="9f24c-325">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="browse-files"></a><span data-ttu-id="9f24c-326">Procurar arquivos</span><span class="sxs-lookup"><span data-stu-id="9f24c-326">Browse files</span></span>
<span data-ttu-id="9f24c-327">Para procurar arquivos armazenados na conta de armazenamento padrão e as contas de armazenamento vinculadas, clique em **Navegador de Arquivos** no console de Consulta do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-327">To browse files stored in the default storage account and the linked storage accounts, click **File Browser** in the HDInsight Query console.</span></span> <span data-ttu-id="9f24c-328">Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="9f24c-328">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

<span data-ttu-id="9f24c-329">Você também pode usar o utilitário **Procurar no sistema de arquivos** da **interface do usuário do Hadoop** no console do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-329">You can also use the **Browse the file system** utility from the **Hadoop UI** in the HDInsight console.</span></span>  <span data-ttu-id="9f24c-330">Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="9f24c-330">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="monitor-cluster-usage"></a><span data-ttu-id="9f24c-331">Monitorar o uso do cluster</span><span class="sxs-lookup"><span data-stu-id="9f24c-331">Monitor cluster usage</span></span>
<span data-ttu-id="9f24c-332">A seção **Uso** da folha do cluster do HDInsight exibe informações sobre o número de núcleos disponíveis para sua assinatura para uso com o HDInsight, bem como o número de núcleos alocados para esse cluster e como eles são alocados para os nós presentes no cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-332">The **Usage** section of the HDInsight cluster blade displays information about the number of cores available to your subscription for use with HDInsight, as well as the number of cores allocated to this cluster and how they are allocated for the nodes within this cluster.</span></span> <span data-ttu-id="9f24c-333">Consulte [Listar e mostrar clusters](#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="9f24c-333">See [List and show clusters](#list-and-show-clusters).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f24c-334">Para monitorar os serviços fornecidos pelo cluster HDInsight, você deve usar o Ambari Web ou a API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="9f24c-334">To monitor the services provided by the HDInsight cluster, you must use Ambari Web or the Ambari REST API.</span></span> <span data-ttu-id="9f24c-335">Para saber mais sobre como usar o Ambari, consulte [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="9f24c-335">For more information on using Ambari, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>
>
>

## <a name="open-hadoop-ui"></a><span data-ttu-id="9f24c-336">Abrir a IU do Hadoop</span><span class="sxs-lookup"><span data-stu-id="9f24c-336">Open Hadoop UI</span></span>
<span data-ttu-id="9f24c-337">Para monitorar o cluster, procure no sistema de arquivos e verifique os logs, clique em **IU do Hadoop** no console de Consulta do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-337">To monitor the cluster, browse the file system, and check logs, click **Hadoop UI** in the HDInsight Query console.</span></span> <span data-ttu-id="9f24c-338">Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="9f24c-338">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="open-yarn-ui"></a><span data-ttu-id="9f24c-339">Abrir a IU do Yarn</span><span class="sxs-lookup"><span data-stu-id="9f24c-339">Open Yarn UI</span></span>
<span data-ttu-id="9f24c-340">Para usar a interface do usuário do Yarn, clique em **Interface do usuário do Yarn** no console de Consulta do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f24c-340">To use Yarn user interface, click **Yarn UI** in the HDInsight Query console.</span></span> <span data-ttu-id="9f24c-341">Consulte [Abrir o console de consulta do HDInsight](#open-hdinsight-query-console).</span><span class="sxs-lookup"><span data-stu-id="9f24c-341">See [Open HDInsight Query console](#open-hdinsight-query-console).</span></span>

## <a name="connect-to-clusters-using-rdp"></a><span data-ttu-id="9f24c-342">Conectar-se aos clusters usando o RDP</span><span class="sxs-lookup"><span data-stu-id="9f24c-342">Connect to clusters using RDP</span></span>
<span data-ttu-id="9f24c-343">As credenciais do cluster que você forneceu em sua criação concedem acesso aos serviços do cluster, mas não ao próprio cluster através da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="9f24c-343">The credentials for the cluster that you provided at its creation give access to the services on the cluster, but not to the cluster itself through Remote Desktop.</span></span> <span data-ttu-id="9f24c-344">Você pode ativar o acesso de Área de Trabalho Remota ao provisionar um cluster ou depois que um cluster for provisionado.</span><span class="sxs-lookup"><span data-stu-id="9f24c-344">You can turn on Remote Desktop access when you provision a cluster or after a cluster is provisioned.</span></span> <span data-ttu-id="9f24c-345">Para obter instruções sobre como habilitar a Área de Trabalho Remota na criação, consulte [Criar cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9f24c-345">For the instructions about enabling Remote Desktop at creation, see [Create HDInsight cluster](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="9f24c-346">**Para habilitar a área de trabalho remota**</span><span class="sxs-lookup"><span data-stu-id="9f24c-346">**To enable Remote Desktop**</span></span>

1. <span data-ttu-id="9f24c-347">Conecte-se no [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f24c-347">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="9f24c-348">Clique em **Procurar Tudo** no menu esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-348">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="9f24c-349">Clique em **Configurações** no menu superior e clique em **Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-349">Click **Settings** from the top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="9f24c-350">Insira **Expira em**, **Nome de Usuário de Área de Trabalho Remota** e **Senha de Área de Trabalho Remota** e clique em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-350">Enter **Expires On**, **Remote Desktop Username** and **Remote Desktop Password**, and then click **Enable**.</span></span>

    ![Habilitar/desabilitar configuração de área de trabalho remota do HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    <span data-ttu-id="9f24c-352">Os valores padrão para Expira em é uma semana.</span><span class="sxs-lookup"><span data-stu-id="9f24c-352">The default values for Expires On is a week.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f24c-353">Você também pode usar o SDK do .NET HDInsight para habilitar a área de trabalho remota em um cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-353">You can also use the HDInsight .NET SDK to enable Remote Desktop on a cluster.</span></span> <span data-ttu-id="9f24c-354">Use o **EnableRdp** método no objeto de cliente HDInsight da seguinte maneira: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-354">Use the **EnableRdp** method on the HDInsight client object in the following manner: **client.EnableRdp(clustername, location, "rdpuser", "rdppassword", DateTime.Now.AddDays(6))**.</span></span> <span data-ttu-id="9f24c-355">Da mesma forma, para desabilitar a área de trabalho remota no cluster, você pode usar **client.DisableRdp(clustername, location)**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-355">Similarly, to disable Remote Desktop on the cluster, you can use **client.DisableRdp(clustername, location)**.</span></span> <span data-ttu-id="9f24c-356">Para obter mais informações sobre esses métodos, consulte [Referência do SDK do .NET HDInsight](http://go.microsoft.com/fwlink/?LinkId=529017).</span><span class="sxs-lookup"><span data-stu-id="9f24c-356">For more information on these methods, see [HDInsight .NET SDK Reference](http://go.microsoft.com/fwlink/?LinkId=529017).</span></span> <span data-ttu-id="9f24c-357">Isso é aplicável apenas a clusters do HDInsight em execução no Windows.</span><span class="sxs-lookup"><span data-stu-id="9f24c-357">This is applicable only for HDInsight clusters running on Windows.</span></span>
   >
   >

<span data-ttu-id="9f24c-358">**Para conectar-se ao cluster usando o RDP**</span><span class="sxs-lookup"><span data-stu-id="9f24c-358">**To connect to a cluster by using RDP**</span></span>

1. <span data-ttu-id="9f24c-359">Conecte-se no [Portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="9f24c-359">Sign in to the [Portal][azure-portal].</span></span>
2. <span data-ttu-id="9f24c-360">Clique em **Procurar Tudo** no menu esquerdo, clique em **Clusters HDInsight**, clique no nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-360">Click **Browse All** from the left menu, click **HDInsight Clusters**, click your cluster name.</span></span>
3. <span data-ttu-id="9f24c-361">Clique em **Configurações** no menu superior e clique em **Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-361">Click **Settings** from the top menu, and then click **Remote Desktop**.</span></span>
4. <span data-ttu-id="9f24c-362">Clique em **Conectar** e siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="9f24c-362">Click **Connect** and follow the instructions.</span></span> <span data-ttu-id="9f24c-363">Se Conectar estiver desabilitado, você deverá habilitá-lo primeiro.</span><span class="sxs-lookup"><span data-stu-id="9f24c-363">If Connect is disable, you must enable it first.</span></span> <span data-ttu-id="9f24c-364">Use o nome do usuário e a senha da Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="9f24c-364">Make sure using the Remote Desktop user username and password.</span></span>  <span data-ttu-id="9f24c-365">Não é possível usar as credenciais de usuário do Cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-365">You can't use the Cluster user credentials.</span></span>

## <a name="open-hadoop-command-line"></a><span data-ttu-id="9f24c-366">Abrir a linha de comando do Hadoop</span><span class="sxs-lookup"><span data-stu-id="9f24c-366">Open Hadoop command line</span></span>
<span data-ttu-id="9f24c-367">Para conectar-se ao cluster usando a área de trabalho remota e usar a linha de comando do Hadoop, você deve primeiro habilitar o acesso à área de trabalho remota para o cluster conforme descrito na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="9f24c-367">To connect to the cluster by using Remote Desktop and use the Hadoop command line, you must first have enabled Remote Desktop access to the cluster as described in the previous section.</span></span>

<span data-ttu-id="9f24c-368">**Para abrir a linha de comando do Hadoop**</span><span class="sxs-lookup"><span data-stu-id="9f24c-368">**To open a Hadoop command line**</span></span>

1. <span data-ttu-id="9f24c-369">Conecte-se ao cluster usando a Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="9f24c-369">Connect to the cluster using Remote Desktop.</span></span>
2. <span data-ttu-id="9f24c-370">Na área de trabalho, clique duas vezes em **Linha de Comando do Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="9f24c-370">From the desktop, double-click **Hadoop Command Line**.</span></span>

    <span data-ttu-id="9f24c-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span><span class="sxs-lookup"><span data-stu-id="9f24c-371">![HDI.HadoopCommandLine][image-hadoopcommandline]</span></span>

    <span data-ttu-id="9f24c-372">Para obter mais informações sobre os comandos Hadoop, consulte [Referência de comandos Hadoop](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span><span class="sxs-lookup"><span data-stu-id="9f24c-372">For more information on Hadoop commands, see [Hadoop commands reference](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).</span></span>

<span data-ttu-id="9f24c-373">Na captura de tela anterior, o nome da pasta tem o número de versão do Hadoop incorporado.</span><span class="sxs-lookup"><span data-stu-id="9f24c-373">In the previous screenshot, the folder name has the Hadoop version number embedded.</span></span> <span data-ttu-id="9f24c-374">O número da versão pode ser alterado com base na versão dos componentes do Hadoop instalados no cluster.</span><span class="sxs-lookup"><span data-stu-id="9f24c-374">The version number can changed based on the version of the Hadoop components installed on the cluster.</span></span> <span data-ttu-id="9f24c-375">Você pode usar variáveis de ambiente do Hadoop para referir-se a essas pastas.</span><span class="sxs-lookup"><span data-stu-id="9f24c-375">You can use Hadoop environment variables to refer to those folders.</span></span> <span data-ttu-id="9f24c-376">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9f24c-376">For example:</span></span>

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a><span data-ttu-id="9f24c-377">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f24c-377">Next steps</span></span>
<span data-ttu-id="9f24c-378">Neste artigo, você aprendeu como criar um cluster HDInsight usando o Portal e como abrir a ferramenta de linha de comando do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9f24c-378">In this article, you have learned how to create an HDInsight cluster by using the Portal, and how to open the Hadoop command-line tool.</span></span> <span data-ttu-id="9f24c-379">Para saber mais, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="9f24c-379">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="9f24c-380">Administrar o HDInsight usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="9f24c-380">Administer HDInsight Using Azure PowerShell</span></span>](hdinsight-administer-use-powershell.md)
* [<span data-ttu-id="9f24c-381">Administrar o HDInsight usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9f24c-381">Administer HDInsight Using Azure CLI</span></span>](hdinsight-administer-use-command-line.md)
* [<span data-ttu-id="9f24c-382">Criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f24c-382">Create HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="9f24c-383">Enviar trabalhos Hadoop de forma programática</span><span class="sxs-lookup"><span data-stu-id="9f24c-383">Submit Hadoop jobs programmatically</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* [<span data-ttu-id="9f24c-384">Introdução ao Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f24c-384">Get Started with Azure HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="9f24c-385">Qual versão do Hadoop está no Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="9f24c-385">What version of Hadoop is in Azure HDInsight?</span></span>](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Linha de comando do Hadoop"
