---
title: "versão mais recente de tooa aaaUpgrade de cluster HDInsight-Azure | Microsoft Docs"
description: "Saiba como tooUpgrade HDInsight cluster tooa nova versão."
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
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="ef8f8-103">Atualizar a versão mais recente de tooa de cluster do HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef8f8-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="ef8f8-104">tootake aproveitar Olá recursos mais recentes do HDInsight, é recomendável que os clusters HDInsight seja atualizado toolatest versão.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="ef8f8-105">Siga Olá abaixo diretrizes tooupgrade suas versões de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="ef8f8-106">Os clusters HDInsight da versão 3.2 e 3.3 estão se aproximando da data de desativação.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="ef8f8-107">Para obter mais informações sobre a versão com suporte do HDInsight, consulte [Versões de componente do HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="ef8f8-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="ef8f8-108">Tarefas de atualização</span><span class="sxs-lookup"><span data-stu-id="ef8f8-108">Upgrade tasks</span></span>
<span data-ttu-id="ef8f8-109">Olá fluxo de trabalho tooupgrade HDInsight Cluster é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Diagrama de fluxo de trabalho de atualização](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="ef8f8-111">Leia cada seção deste documento toounderstand alterações que podem ser necessárias ao atualizar seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="ef8f8-112">Crie um cluster como um ambiente de teste/garantia de qualidade.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="ef8f8-113">Para obter mais informações sobre como criar um cluster, consulte [Saiba como toocreate HDInsight baseados em Linux clusters](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="ef8f8-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="ef8f8-114">Cópia existente de trabalhos, fontes de dados e coletores toohello novo ambiente.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="ef8f8-115">Consulte [tooTest copiar dados ambiente](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="ef8f8-116">Execute testes toomake se os trabalhos funcionam conforme esperado no cluster novo Olá de validação.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="ef8f8-117">Depois de ter verificado que tudo está funcionando conforme o esperado, agende o tempo de inatividade para migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="ef8f8-118">Durante esse tempo de inatividade, Olá seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="ef8f8-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="ef8f8-119">Fazer backup dos dados transitórios armazenados localmente em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="ef8f8-120">Por exemplo, se você tiver dados armazenados diretamente em um nó principal.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="ef8f8-121">Exclua o cluster existente hello.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="ef8f8-122">Criar um cluster em Olá mesmo VNET sub-rede com mais recente (ou compatíveis) HDI versão usando Olá mesmo repositório de dados padrão que Olá cluster anterior usado.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="ef8f8-123">Isso permite Olá novo cluster toocontinue trabalham com os dados de produção existentes.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="ef8f8-124">Importe o backup de todos os dados transitórios.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="ef8f8-125">Iniciar trabalhos/continuar o processamento usando o novo cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef8f8-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef8f8-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef8f8-126">Next Steps</span></span>
* [<span data-ttu-id="ef8f8-127">Saiba como toocreate HDInsight baseados em Linux clusters</span><span class="sxs-lookup"><span data-stu-id="ef8f8-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="ef8f8-128">Conecte-se tooHDInsight usando SSH</span><span class="sxs-lookup"><span data-stu-id="ef8f8-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="ef8f8-129">Gerenciar um cluster baseado em Linux usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="ef8f8-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

