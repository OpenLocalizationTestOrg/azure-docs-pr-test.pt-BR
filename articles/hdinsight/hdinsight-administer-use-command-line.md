---
title: clusters de Hadoop aaaManage usando a CLI do Azure - HDInsight do Azure | Microsoft Docs
description: "Saiba como clusters de toouse Olá Interface de linha de comando do Azure toomanage Hadoop no HDInsight do Azure. Olá CLI do Azure funciona no Windows, Mac e Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a><span data-ttu-id="e1ef8-104">Gerenciar clusters Hadoop em HDInsight usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e1ef8-104">Manage Hadoop clusters in HDInsight using hello Azure CLI</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="e1ef8-105">Saiba como Olá toouse [Interface de linha de comando do Azure](../cli-install-nodejs.md) toomanage Hadoop clusters de HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-105">Learn how toouse hello [Azure Command-line Interface](../cli-install-nodejs.md) toomanage Hadoop clusters in Azure HDInsight.</span></span> <span data-ttu-id="e1ef8-106">Olá CLI do Azure é implementada no Node. js.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-106">hello Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="e1ef8-107">Ela pode ser usada em qualquer plataforma que dê suporte ao Node.js, incluindo Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-107">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span>

<span data-ttu-id="e1ef8-108">Este artigo aborda apenas com hello CLI do Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-108">This article covers only using hello Azure CLI with HDInsight.</span></span> <span data-ttu-id="e1ef8-109">Para obter um guia geral sobre como toouse CLI do Azure, consulte [instalar e configurar a CLI do Azure][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="e1ef8-109">For a general guide on how toouse Azure CLI, see [Install and configure Azure CLI][azure-command-line-tools].</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a><span data-ttu-id="e1ef8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e1ef8-110">Prerequisites</span></span>
<span data-ttu-id="e1ef8-111">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-111">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="e1ef8-112">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-112">**An Azure subscription**.</span></span> <span data-ttu-id="e1ef8-113">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e1ef8-113">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e1ef8-114">**CLI do Azure** -consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) para obter informações de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-114">**Azure CLI** - See [Install and configure hello Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span>
* <span data-ttu-id="e1ef8-115">**Conecte-se tooAzure**usando Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-115">**Connect tooAzure**, using hello following command:</span></span>
  
        azure login
  
    <span data-ttu-id="e1ef8-116">Para obter mais informações sobre autenticação usando uma conta corporativa ou escolar, consulte [conectar tooan assinatura do Azure do hello CLI do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e1ef8-116">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="e1ef8-117">**Modo do comutador toohello Azure Resource Manager**usando Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-117">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="e1ef8-118">tooget ajuda, use Olá **-h** alternar.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-118">tooget help, use hello **-h** switch.</span></span>  <span data-ttu-id="e1ef8-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-119">For example:</span></span>

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a><span data-ttu-id="e1ef8-120">Criar clusters com hello CLI</span><span class="sxs-lookup"><span data-stu-id="e1ef8-120">Create clusters with hello CLI</span></span>
<span data-ttu-id="e1ef8-121">Consulte [criar clusters HDInsight usando Olá CLI do Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e1ef8-121">See [Create clusters in HDInsight using hello Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md).</span></span>

## <a name="list-and-show-cluster-details"></a><span data-ttu-id="e1ef8-122">Listar e mostrar detalhes do cluster</span><span class="sxs-lookup"><span data-stu-id="e1ef8-122">List and show cluster details</span></span>
<span data-ttu-id="e1ef8-123">Use Olá toolist comandos a seguir e mostrar os detalhes do cluster:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-123">Use hello following commands toolist and show cluster details:</span></span>

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

<span data-ttu-id="e1ef8-124">![Modo de exibição de linha de comando de lista de clusters][image-cli-clusterlisting]</span><span class="sxs-lookup"><span data-stu-id="e1ef8-124">![Command-line view of cluster list][image-cli-clusterlisting]</span></span>

## <a name="delete-clusters"></a><span data-ttu-id="e1ef8-125">Excluir clusters</span><span class="sxs-lookup"><span data-stu-id="e1ef8-125">Delete clusters</span></span>
<span data-ttu-id="e1ef8-126">Use Olá comando toodelete um cluster a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-126">Use hello following command toodelete a cluster:</span></span>

    azure hdinsight cluster delete <Cluster Name>

<span data-ttu-id="e1ef8-127">Você também pode excluir um cluster, excluindo o grupo de recursos de saudação que contém o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-127">You can also delete a cluster by deleting hello resource group that contains hello cluster.</span></span> <span data-ttu-id="e1ef8-128">Observe que isso excluirá todos os recursos de saudação no grupo de hello, incluindo a conta de armazenamento padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-128">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="e1ef8-129">Dimensionar clusters</span><span class="sxs-lookup"><span data-stu-id="e1ef8-129">Scale clusters</span></span>
<span data-ttu-id="e1ef8-130">Olá toochange tamanho do cluster Hadoop:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-130">toochange hello Hadoop cluster size:</span></span>

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a><span data-ttu-id="e1ef8-131">Habilitar/desabilitar o acesso HTTP para um cluster</span><span class="sxs-lookup"><span data-stu-id="e1ef8-131">Enable/disable HTTP access for a cluster</span></span>
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a><span data-ttu-id="e1ef8-132">Habilitar/desabilitar o acesso RDP para um cluster</span><span class="sxs-lookup"><span data-stu-id="e1ef8-132">Enable/disable RDP access for a cluster</span></span>
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a><span data-ttu-id="e1ef8-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1ef8-133">Next steps</span></span>
<span data-ttu-id="e1ef8-134">Neste artigo, você aprendeu como tooperform HDInsight cluster tarefas administrativas.</span><span class="sxs-lookup"><span data-stu-id="e1ef8-134">In this article, you have learned how tooperform different HDInsight cluster administrative tasks.</span></span> <span data-ttu-id="e1ef8-135">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1ef8-135">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="e1ef8-136">[Administrar HDInsight usando Olá Portal do Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="e1ef8-136">[Administer HDInsight by using hello Azure Portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="e1ef8-137">[Administrar clusters HDInsight usando o Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="e1ef8-137">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="e1ef8-138">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e1ef8-138">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="e1ef8-139">[Como toouse Olá CLI do Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="e1ef8-139">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Listar e mostrar clusters"
