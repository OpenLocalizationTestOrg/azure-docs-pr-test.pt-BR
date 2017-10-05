---
title: Alta disponibilidade com o Apache Kafka - Azure HDInsight | Microsoft Docs
description: "Saiba como garantir a alta disponibilidade com o Apache Kafka no Azure HDInsight. Saiba como reequilibrar réplicas da partição no Kafka para que eles fiquem em domínios de falha diferentes dentro da região do Azure que contém o HDInsight."
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
ms.openlocfilehash: f8164d1c3483b28e5f2abcc8035da78880daec1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="f4870-104">Alta disponibilidade de seus dados com o Apache Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4870-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="f4870-105">Saiba como configurar réplicas da partição para tópicos Kafka a fim de tirar proveito da configuração de rack do hardware subjacente.</span><span class="sxs-lookup"><span data-stu-id="f4870-105">Learn how to configure partition replicas for Kafka topics to take advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="f4870-106">Essa configuração garante a disponibilidade dos dados armazenados no Apache Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f4870-106">This configuration ensures the availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="f4870-107">Domínios de falha e atualização com Kafka</span><span class="sxs-lookup"><span data-stu-id="f4870-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="f4870-108">Um domínio de falha é um agrupamento lógico de hardware subjacente em um data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4870-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="f4870-109">Cada domínio de falha tem um comutador de rede e uma fonte de alimentação em comum.</span><span class="sxs-lookup"><span data-stu-id="f4870-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="f4870-110">As máquinas virtuais e os discos gerenciados que implementam os nós em um cluster HDInsight são distribuídos entre esses domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="f4870-110">The virtual machines and managed disks that implement the nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="f4870-111">Essa arquitetura limita o possível impacto de falhas físicas de hardware.</span><span class="sxs-lookup"><span data-stu-id="f4870-111">This architecture limits the potential impact of physical hardware failures.</span></span>

<span data-ttu-id="f4870-112">Cada região do Azure tem um número específico de domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="f4870-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="f4870-113">Para obter uma lista de domínios e a quantidade de domínios de falha que eles contêm, confira a documentação [conjuntos de disponibilidade](../virtual-machines/linux/regions-and-availability.md#availability-sets).</span><span class="sxs-lookup"><span data-stu-id="f4870-113">For a list of domains and the number of fault domains they contain, see the [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4870-114">O Kafka não está ciente dos domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="f4870-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="f4870-115">Quando você cria um tópico no Kafka, ele pode armazenar todas as réplicas da partição no mesmo domínio de falha.</span><span class="sxs-lookup"><span data-stu-id="f4870-115">When you create a topic in Kafka, it may store all partition replicas in the same fault domain.</span></span> <span data-ttu-id="f4870-116">Para resolver esse problema, fornecemos a [ferramenta de rebalanceamento de partição do Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="f4870-116">To solve this problem, we provide the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-to-rebalance-partition-replicas"></a><span data-ttu-id="f4870-117">Quando rebalancear réplicas da partição</span><span class="sxs-lookup"><span data-stu-id="f4870-117">When to rebalance partition replicas</span></span>

<span data-ttu-id="f4870-118">Para garantir a mais alta disponibilidade de seus dados do Kafka, você deve rebalancear as réplicas de partição do tópico nas seguintes situações:</span><span class="sxs-lookup"><span data-stu-id="f4870-118">To ensure the highest availability of your Kafka data, you should rebalance the partition replicas for your topic at the following times:</span></span>

* <span data-ttu-id="f4870-119">Quando um novo tópico ou uma partição é criado</span><span class="sxs-lookup"><span data-stu-id="f4870-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="f4870-120">Quando você expande um cluster</span><span class="sxs-lookup"><span data-stu-id="f4870-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="f4870-121">Fator de replicação</span><span class="sxs-lookup"><span data-stu-id="f4870-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4870-122">É recomendável usar uma região do Azure que contenha três domínios de falha e um fator de replicação de 3.</span><span class="sxs-lookup"><span data-stu-id="f4870-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="f4870-123">Se você precisa usar uma região que contém apenas dois domínios de falha, use um fator de replicação de 4 para distribuir as réplicas uniformemente entre os dois domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="f4870-123">If you must use a region that contains only two fault domains, use a replication factor of 4 to spread the replicas evenly across the two fault domains.</span></span>

<span data-ttu-id="f4870-124">Para obter um exemplo como criar tópicos e configurar o fator de replicação, consulte o documento [Introdução ao Kafka no HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f4870-124">For an example of creating topics and setting the replication factor, see the [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-to-rebalance-partition-replicas"></a><span data-ttu-id="f4870-125">Como rebalancear réplicas da partição</span><span class="sxs-lookup"><span data-stu-id="f4870-125">How to rebalance partition replicas</span></span>

<span data-ttu-id="f4870-126">Use a [ferramenta de rebalanceamento de partição do Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) para rebalancear tópicos selecionados.</span><span class="sxs-lookup"><span data-stu-id="f4870-126">Use the [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) to rebalance selected topics.</span></span> <span data-ttu-id="f4870-127">Essa ferramenta deve ser executada em uma sessão SSH para o nó principal do cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="f4870-127">This tool must be ran from an SSH session to the head node of your Kafka cluster.</span></span>

<span data-ttu-id="f4870-128">Para saber mais sobre como se conectar ao HDInsight usando SSH, consulte o documento [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f4870-128">For more information on connecting to HDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4870-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4870-129">Next steps</span></span>

* [<span data-ttu-id="f4870-130">Escalabilidade do Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4870-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="f4870-131">Espelhamento com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f4870-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)