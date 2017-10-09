---
title: "Introdução de aaaAn tooApache Kafka no HDInsight - Azure | Microsoft Docs"
description: "Saiba mais sobre o Apache Kafka no HDInsight: o que é, o que ele faz e onde os exemplos de toofind e introdução a informações."
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
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="caa23-103">Introdução ao Apache Kafka no HDInsight (visualização)</span><span class="sxs-lookup"><span data-stu-id="caa23-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="caa23-104">[Apache Kafka](https://kafka.apache.org) é uma plataforma de streaming distribuído código-fonte aberto que pode ser usadas em tempo real de toobuild streaming pipelines de dados e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="caa23-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="caa23-105">Kafka também fornece o agente de mensagem funcionalidade semelhante tooa fila de mensagens, onde você pode publicar e assinar toonamed fluxos de dados.</span><span class="sxs-lookup"><span data-stu-id="caa23-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="caa23-106">Kafka no HDInsight fornece um serviço gerenciado, altamente disponível e altamente escalonável na nuvem do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="caa23-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="caa23-107">Por que usar o Kafka no HDInsight?</span><span class="sxs-lookup"><span data-stu-id="caa23-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="caa23-108">Kafka fornece Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="caa23-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="caa23-109">Padrão de mensagens de publicação / assinatura: Kafka fornece uma API de produtor para publicar registros tooa tópico Kafka.</span><span class="sxs-lookup"><span data-stu-id="caa23-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="caa23-110">Olá API de consumidor é usado durante a assinatura de tópico tooa.</span><span class="sxs-lookup"><span data-stu-id="caa23-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="caa23-111">Processamento de fluxo: o Kafka é frequentemente usado com o Apache Storm ou o Spark para processamento de fluxo em tempo real.</span><span class="sxs-lookup"><span data-stu-id="caa23-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="caa23-112">Kafka 0.10.0.0 (HDInsight versão 3.5) introduziu uma API de streaming que permite que você toobuild streaming soluções sem a necessidade de tempestade ou Spark.</span><span class="sxs-lookup"><span data-stu-id="caa23-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="caa23-113">Escala horizontal: Kafka particiona fluxos em nós de saudação no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="caa23-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="caa23-114">Processos de consumidor podem ser associados a partições individuais tooprovide balanceamento de carga durante o consumo de registros.</span><span class="sxs-lookup"><span data-stu-id="caa23-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="caa23-115">Entrega em ordem: dentro de cada partição, os registros são armazenados no fluxo de saudação na ordem de saudação que foram recebidos.</span><span class="sxs-lookup"><span data-stu-id="caa23-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="caa23-116">Ao associar um processo do consumidor por partição, você pode garantir que os registros sejam processados na ordem.</span><span class="sxs-lookup"><span data-stu-id="caa23-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="caa23-117">Tolerância: Partições podem ser replicadas entre a tolerância a falhas de tooprovide nós.</span><span class="sxs-lookup"><span data-stu-id="caa23-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="caa23-118">Integração com o Azure gerenciados discos: discos gerenciado fornece maior escala e taxa de transferência para discos de saudação usados nas máquinas virtuais no cluster do HDInsight Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="caa23-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="caa23-119">Discos gerenciados são habilitados por padrão para Kafka no HDInsight e número de saudação de discos usados por nó pode ser configurado durante a criação de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="caa23-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="caa23-120">Para saber mais sobre discos gerenciados, veja [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="caa23-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="caa23-121">Para saber mais sobre como configurar discos gerenciados com o Kafka no HDInsight, veja [Aumentar a escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="caa23-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="caa23-122">Casos de uso</span><span class="sxs-lookup"><span data-stu-id="caa23-122">Use cases</span></span>

* <span data-ttu-id="caa23-123">**Mensagens**: uma vez que ele dá suporte a saudação padrão de mensagens de publicação / assinatura, Kafka geralmente é usada como um agente de mensagens.</span><span class="sxs-lookup"><span data-stu-id="caa23-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="caa23-124">**Atividade de controle**: Kafka desde que fornece o registro em log na ordem de registros, pode ser usado tootrack e crie novamente as atividades.</span><span class="sxs-lookup"><span data-stu-id="caa23-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="caa23-125">Por exemplo, as ações do usuário em um site ou em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="caa23-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="caa23-126">**Agregação**: usando processamento de fluxo, você pode agregar informações de fluxos diferentes toocombine e centralizar Olá informações em dados operacionais.</span><span class="sxs-lookup"><span data-stu-id="caa23-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="caa23-127">**Transformação**: usando processamento de fluxo, você pode combinar e enriquecer dados de vários tópicos de entrada em um ou mais tópicos de saída.</span><span class="sxs-lookup"><span data-stu-id="caa23-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caa23-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="caa23-128">Next steps</span></span>

<span data-ttu-id="caa23-129">Links a seguir do uso Olá toolearn como toouse Kafka do Apache no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="caa23-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="caa23-130">Introdução ao Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="caa23-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="caa23-131">Use MirrorMaker toocreate uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="caa23-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="caa23-132">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="caa23-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="caa23-133">Usar o Apache Spark com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="caa23-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="caa23-134">Conecte-se tooKafka por meio de uma rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="caa23-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
