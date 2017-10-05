---
title: Escala de aumento do Apache Kafka - Azure HDInsight | Microsoft Docs
description: Saiba como configurar discos gerenciados para o cluster Apache Kafka no Azure HDInsight para aumentar a escalabilidade.
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: 880a186a3d9a23b013294b0121e8265270d160cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="b7aee-103">Configurar o armazenamento e a escalabilidade para o Apache Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7aee-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="b7aee-104">Saiba como configurar o número de discos gerenciados usados pelo Apache Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7aee-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="b7aee-105">O Kafka no HDInsight usa o disco local das máquinas virtuais no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7aee-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span></span> <span data-ttu-id="b7aee-106">Como o Kafka tem E/S bastante pesadas, os [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) são usados para fornecer a alta taxa de transferência e fornecer mais armazenamento por nó.</span><span class="sxs-lookup"><span data-stu-id="b7aee-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span></span> <span data-ttu-id="b7aee-107">Se os discos rígidos virtuais (VHD) tradicionais tiverem sido usados para o Kafka, cada nó estará limitado a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="b7aee-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span></span> <span data-ttu-id="b7aee-108">Com os discos gerenciados, você pode usar vários discos para alcançar 16 TB para cada nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="b7aee-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span></span>

<span data-ttu-id="b7aee-109">O diagrama a seguir fornece uma comparação entre o Kafka no HDInsight antes dos discos gerenciados e o Kafka no HDInsight com os discos gerenciados:</span><span class="sxs-lookup"><span data-stu-id="b7aee-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagrama mostrando o Kafka no HDInsight usando um único vhd por vm versus vários discos gerenciados por vm](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="b7aee-111">Configurar discos gerenciados: portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b7aee-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="b7aee-112">Siga as etapas de [Criar um cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) para compreender as etapas comuns para criar um cluster usando o portal.</span><span class="sxs-lookup"><span data-stu-id="b7aee-112">Follow the steps in the [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span></span> <span data-ttu-id="b7aee-113">Não conclua o processo de criação do portal.</span><span class="sxs-lookup"><span data-stu-id="b7aee-113">Do not complete the portal creation process.</span></span>

2. <span data-ttu-id="b7aee-114">Na folha __Tamanho do cluster__, use o campo __Discos por nó de trabalho__ para configurar o número de discos.</span><span class="sxs-lookup"><span data-stu-id="b7aee-114">From the __Cluster size__ blade, use the __Disks per worker node__ field to configure the number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7aee-115">O tipo de disco gerenciado pode ser __Standard__ (HDD) ou __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="b7aee-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="b7aee-116">Os discos Premium são usados com as VMs das séries DS e GS.</span><span class="sxs-lookup"><span data-stu-id="b7aee-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="b7aee-117">Todos os outros tipos VM usam o padrão.</span><span class="sxs-lookup"><span data-stu-id="b7aee-117">All other VM types use standard.</span></span>

    ![Imagem da folha de tamanho de cluster com os discos por nó de trabalho realçados](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="b7aee-119">Configurar discos gerenciados: modelo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="b7aee-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="b7aee-120">Para controlar o número de discos usados por nós de trabalho em um cluster do Kafka, use a seção a seguir do modelo:</span><span class="sxs-lookup"><span data-stu-id="b7aee-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="b7aee-121">Você pode encontrar um modelo completo que demonstra como configurar os discos gerenciados em [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="b7aee-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7aee-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7aee-122">Next steps</span></span>

<span data-ttu-id="b7aee-123">Para saber mais sobre como trabalhar com o Kafka no HDInsight, veja os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="b7aee-123">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="b7aee-124">Usar MirrorMaker para criar uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7aee-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="b7aee-125">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7aee-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="b7aee-126">Usar o Apache Spark com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7aee-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="b7aee-127">Conectar-se ao Kafka no HDInsight (preview) por meio de uma Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="b7aee-127">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="b7aee-128">Blog do HDInsight em discos gerenciados com o Kafka</span><span class="sxs-lookup"><span data-stu-id="b7aee-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)