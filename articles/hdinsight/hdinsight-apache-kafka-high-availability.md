---
title: disponibilidade de aaaHigh com Kafka Apache - HDInsight do Azure | Microsoft Docs
description: "Saiba como tooensure alta disponibilidade com o Apache Kafka no Azure HDInsight. Saiba como toorebalance partição réplicas em Kafka para que fiquem em diferentes domínios de falha em Olá região do Azure que contém o HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="270a6-104">Alta disponibilidade de seus dados com o Apache Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="270a6-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="270a6-105">Saiba como réplicas da partição tooconfigure para Kafka tópicos tootake aproveitar hardware subjacente rack configuração.</span><span class="sxs-lookup"><span data-stu-id="270a6-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="270a6-106">Essa configuração garante a disponibilidade de saudação dos dados armazenados no Apache Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270a6-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="270a6-107">Domínios de falha e atualização com Kafka</span><span class="sxs-lookup"><span data-stu-id="270a6-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="270a6-108">Um domínio de falha é um agrupamento lógico de hardware subjacente em um data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="270a6-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="270a6-109">Cada domínio de falha tem um comutador de rede e uma fonte de alimentação em comum.</span><span class="sxs-lookup"><span data-stu-id="270a6-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="270a6-110">máquinas virtuais de saudação e discos gerenciados que implementa nós hello dentro de um cluster HDInsight são distribuídos entre esses domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="270a6-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="270a6-111">Essa arquitetura limita o impacto potencial de saudação de falhas de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="270a6-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="270a6-112">Cada região do Azure tem um número específico de domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="270a6-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="270a6-113">Para obter uma lista de domínios e número de saudação de domínios de falha que eles contêm, consulte Olá [conjuntos de disponibilidade](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentação.</span><span class="sxs-lookup"><span data-stu-id="270a6-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="270a6-114">O Kafka não está ciente dos domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="270a6-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="270a6-115">Quando você cria um tópico no Kafka, ele pode armazenar todas as réplicas de partição em Olá mesmo domínio de falha.</span><span class="sxs-lookup"><span data-stu-id="270a6-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="270a6-116">toosolve esse problema, fornecemos Olá [ferramenta de rebalanceie de partição Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="270a6-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="270a6-117">Quando toorebalance réplicas da partição</span><span class="sxs-lookup"><span data-stu-id="270a6-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="270a6-118">tooensure hello mais alta disponibilidade de seus dados Kafka, você deve reequilibrar réplicas da partição Olá para seu tópico em Olá vezes a seguir:</span><span class="sxs-lookup"><span data-stu-id="270a6-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="270a6-119">Quando um novo tópico ou uma partição é criado</span><span class="sxs-lookup"><span data-stu-id="270a6-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="270a6-120">Quando você expande um cluster</span><span class="sxs-lookup"><span data-stu-id="270a6-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="270a6-121">Fator de replicação</span><span class="sxs-lookup"><span data-stu-id="270a6-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="270a6-122">É recomendável usar uma região do Azure que contenha três domínios de falha e um fator de replicação de 3.</span><span class="sxs-lookup"><span data-stu-id="270a6-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="270a6-123">Se você precisar usar uma região que contém apenas dois domínios de falha, use um fator de replicação de 4 réplicas de saudação toospread uniformemente entre os dois domínios de falha hello.</span><span class="sxs-lookup"><span data-stu-id="270a6-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="270a6-124">Para obter um exemplo de criação de tópicos e o fator de replicação de saudação de configuração, consulte Olá [iniciar com Kafka no HDInsight](hdinsight-apache-kafka-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="270a6-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="270a6-125">Como a partição toorebalance réplicas</span><span class="sxs-lookup"><span data-stu-id="270a6-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="270a6-126">Saudação de uso [ferramenta de rebalanceie de partição Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selecionado tópicos.</span><span class="sxs-lookup"><span data-stu-id="270a6-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="270a6-127">Essa ferramenta deve ser executado de um nó SSH sessão toohello principal do cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="270a6-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="270a6-128">Para obter mais informações sobre como conectar tooHDInsight usando SSH, consulte o [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="270a6-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="270a6-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="270a6-129">Next steps</span></span>

* [<span data-ttu-id="270a6-130">Escalabilidade do Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="270a6-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="270a6-131">Espelhamento com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="270a6-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)