---
title: "Uma introdução ao Apache Kafka no HDInsight - Azure | Microsoft Docs"
description: "Saiba mais sobre o Apache Kafka no HDInsight: o que é o que ele faz e onde encontrar exemplos e informações de introdução."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1976c52bd7fa56bb07104e205ab3699b2dfa4c50
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="abb11-103">Introdução ao Apache Kafka no HDInsight (visualização)</span><span class="sxs-lookup"><span data-stu-id="abb11-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="abb11-104">O [Apache Kafka](https://kafka.apache.org) é uma plataforma de streaming distribuída de software livre que pode ser usada para compilar pipelines e aplicativos de dados de streaming em tempo real.</span><span class="sxs-lookup"><span data-stu-id="abb11-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used to build real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="abb11-105">O Kafka também fornece funcionalidade de agente de mensagem semelhante a uma fila de mensagens, onde você pode publicar e assinar os fluxos de dados nomeados.</span><span class="sxs-lookup"><span data-stu-id="abb11-105">Kafka also provides message broker functionality similar to a message queue, where you can publish and subscribe to named data streams.</span></span> <span data-ttu-id="abb11-106">O Kafka no HDInsight oferece um serviço gerenciado, altamente escalonável e altamente disponível na nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="abb11-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in the Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="abb11-107">Por que usar o Kafka no HDInsight?</span><span class="sxs-lookup"><span data-stu-id="abb11-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="abb11-108">O Kafka fornece as seguintes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="abb11-108">Kafka provides the following features:</span></span>

* <span data-ttu-id="abb11-109">Padrão de mensagens publicar-assinar: o Kafka fornece uma API de Produtor para publicação de registros em um tópico do Kafka.</span><span class="sxs-lookup"><span data-stu-id="abb11-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records to a Kafka topic.</span></span> <span data-ttu-id="abb11-110">A API de Consumidor é usada na assinatura de um tópico.</span><span class="sxs-lookup"><span data-stu-id="abb11-110">The Consumer API is used when subscribing to a topic.</span></span>

* <span data-ttu-id="abb11-111">Processamento de fluxo: o Kafka é frequentemente usado com o Apache Storm ou o Spark para processamento de fluxo em tempo real.</span><span class="sxs-lookup"><span data-stu-id="abb11-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="abb11-112">O Kafka 0.10.0.0 (HDInsight versão 3.5) introduziu uma API de streaming que permite que você crie soluções de transmissão sem a necessidade do Storm ou do Spark.</span><span class="sxs-lookup"><span data-stu-id="abb11-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you to build streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="abb11-113">Escala horizontal: o Kafka particiona fluxos entre os nós no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abb11-113">Horizontal scale: Kafka partitions streams across the nodes in the HDInsight cluster.</span></span> <span data-ttu-id="abb11-114">Os processos do Consumidor podem ser associados a partições individuais para fornecer balanceamento de carga ao consumir registros.</span><span class="sxs-lookup"><span data-stu-id="abb11-114">Consumer processes can be associated with individual partitions to provide load balancing when consuming records.</span></span>

* <span data-ttu-id="abb11-115">Entrega em ordem: dentro de cada partição, os registros são armazenados no fluxo na ordem em que foram recebidos.</span><span class="sxs-lookup"><span data-stu-id="abb11-115">In-order delivery: Within each partition, records are stored in the stream in the order that they were received.</span></span> <span data-ttu-id="abb11-116">Ao associar um processo do consumidor por partição, você pode garantir que os registros sejam processados na ordem.</span><span class="sxs-lookup"><span data-stu-id="abb11-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="abb11-117">Tolerante a falhas: as partições podem ser replicadas entre nós para fornecer tolerância a falhas.</span><span class="sxs-lookup"><span data-stu-id="abb11-117">Fault-tolerant: Partitions can be replicated between nodes to provide fault tolerance.</span></span>

* <span data-ttu-id="abb11-118">Integração com os Azure Managed Disks: os discos gerenciados fornecem maior escala e taxa de transferência para os discos usados pelas máquinas virtuais no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abb11-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for the disks used by the virtual machines in the HDInsight cluster.</span></span>

    <span data-ttu-id="abb11-119">Os discos gerenciados são habilitados por padrão para o Kafka no HDInsight e o número de discos usados por nó pode ser configurado durante a criação do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="abb11-119">Managed disks are enabled by default for Kafka on HDInsight, and the number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="abb11-120">Para saber mais sobre discos gerenciados, veja [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="abb11-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="abb11-121">Para saber mais sobre como configurar discos gerenciados com o Kafka no HDInsight, veja [Aumentar a escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="abb11-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="abb11-122">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="abb11-122">Use cases</span></span>

* <span data-ttu-id="abb11-123">**Mensagens**: já que ele oferece suporte ao padrão de mensagem publicar-assinar, o Kafka geralmente é usado como um agente de mensagem.</span><span class="sxs-lookup"><span data-stu-id="abb11-123">**Messaging**: Since it supports the publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="abb11-124">**Rastreamento de atividades**: como o Kafka oferece o registro em log ordenado de registros, pode ser usado para rastrear e recriar as atividades.</span><span class="sxs-lookup"><span data-stu-id="abb11-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used to track and re-create activities.</span></span> <span data-ttu-id="abb11-125">Por exemplo, as ações do usuário em um site ou em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="abb11-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="abb11-126">**Agregação**: usando processamento de fluxo, você pode agregar informações de fluxos diferentes para combinar e centralizar as informações em dados operacionais.</span><span class="sxs-lookup"><span data-stu-id="abb11-126">**Aggregation**: Using stream processing, you can aggregate information from different streams to combine and centralize the information into operational data.</span></span>

* <span data-ttu-id="abb11-127">**Transformação**: usando processamento de fluxo, você pode combinar e enriquecer dados de vários tópicos de entrada em um ou mais tópicos de saída.</span><span class="sxs-lookup"><span data-stu-id="abb11-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abb11-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abb11-128">Next steps</span></span>

<span data-ttu-id="abb11-129">Use os links a seguir para aprender a usar o Apache Kafka no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="abb11-129">Use the following links to learn how to use Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="abb11-130">Introdução ao Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="abb11-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="abb11-131">Usar MirrorMaker para criar uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="abb11-131">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="abb11-132">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="abb11-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="abb11-133">Usar o Apache Spark com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="abb11-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="abb11-134">Conectar-se ao Kafka no HDInsight (preview) por meio de uma Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="abb11-134">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)