---
title: "Atualizar o cluster HDInsight para uma versão mais nova – Azure | Microsoft Docs"
description: "Saiba como atualizar o cluster HDInsight para uma versão mais nova."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="352d2-103">Atualizar o cluster HDInsight para uma versão mais recente</span><span class="sxs-lookup"><span data-stu-id="352d2-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="352d2-104">Para aproveitar os novos recursos do HDInsight, é recomendável que os clusters HDInsight sejam atualizados para a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="352d2-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="352d2-105">Siga as diretrizes apresentadas abaixo para atualizar as versões do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="352d2-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="352d2-106">Os clusters HDInsight da versão 3.2 e 3.3 estão se aproximando da data de desativação.</span><span class="sxs-lookup"><span data-stu-id="352d2-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="352d2-107">Para obter mais informações sobre a versão com suporte do HDInsight, consulte [Versões de componente do HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="352d2-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="352d2-108">Tarefas de atualização</span><span class="sxs-lookup"><span data-stu-id="352d2-108">Upgrade tasks</span></span>
<span data-ttu-id="352d2-109">O fluxo de trabalho para atualizar o cluster HDInsight serão apresentadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="352d2-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Diagrama de fluxo de trabalho de atualização](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="352d2-111">Leia cada seção deste documento para entender as alterações que podem ser necessárias ao atualizar o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="352d2-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="352d2-112">Crie um cluster como um ambiente de teste/garantia de qualidade.</span><span class="sxs-lookup"><span data-stu-id="352d2-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="352d2-113">Para saber mais sobre como criar um cluster, consulte [Saiba como criar clusters HDInsight baseados em Linux](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="352d2-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="352d2-114">Copie trabalhos, fontes de dados e coletores existentes para o novo ambiente.</span><span class="sxs-lookup"><span data-stu-id="352d2-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="352d2-115">Consulte [Copiar Dados para o Ambiente de Teste](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="352d2-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="352d2-116">Execute testes de validação para garantir que os trabalhos funcionem conforme o esperado no novo cluster.</span><span class="sxs-lookup"><span data-stu-id="352d2-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="352d2-117">Depois de verificar se tudo está funcionando conforme o esperado, agende o tempo de inatividade para a migração.</span><span class="sxs-lookup"><span data-stu-id="352d2-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="352d2-118">Durante esse tempo de inatividade, execute as tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="352d2-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="352d2-119">Faça backup de dados transitórios armazenados localmente em nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="352d2-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="352d2-120">Por exemplo, se você tiver dados armazenados diretamente em um nó principal.</span><span class="sxs-lookup"><span data-stu-id="352d2-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="352d2-121">Exclua o cluster existente.</span><span class="sxs-lookup"><span data-stu-id="352d2-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="352d2-122">Crie um cluster na mesma sub-rede VNET com a versão do HDI mais recente (ou com suporte) que usa o mesmo armazenamento de dados padrão utilizado pelo cluster anterior.</span><span class="sxs-lookup"><span data-stu-id="352d2-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="352d2-123">Isso permite que o novo cluster continue trabalhando nos dados de produção existentes.</span><span class="sxs-lookup"><span data-stu-id="352d2-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="352d2-124">Importe o backup de todos os dados transitórios.</span><span class="sxs-lookup"><span data-stu-id="352d2-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="352d2-125">Inicie os trabalhos/continue processando usando o novo cluster.</span><span class="sxs-lookup"><span data-stu-id="352d2-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="352d2-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="352d2-126">Next Steps</span></span>
* [<span data-ttu-id="352d2-127">Saiba como criar clusters HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="352d2-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="352d2-128">Conectar-se ao HDInsight usando o SSH</span><span class="sxs-lookup"><span data-stu-id="352d2-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="352d2-129">Gerenciar um cluster baseado em Linux usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="352d2-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

