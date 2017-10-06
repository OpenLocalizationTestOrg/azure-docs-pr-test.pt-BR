---
title: aaaApache Kafka aumentar a escala - HDInsight do Azure | Microsoft Docs
description: Saiba como tooconfigure gerenciada discos de cluster Kafka do Apache no Azure HDInsight tooincrease escalabilidade.
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
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="0d3a8-103">Configurar o armazenamento e a escalabilidade para o Apache Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d3a8-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="0d3a8-104">Saiba como número de saudação tooconfigure de discos gerenciados usados pelo Apache Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="0d3a8-105">Kafka no HDInsight usa a disco local Olá de máquinas virtuais de saudação no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="0d3a8-106">Como Kafka é bastante e/s pesados, [discos gerenciado do Azure](../virtual-machines/windows/managed-disks-overview.md) é usado tooprovide alta taxa de transferência e fornece mais armazenamento por nó.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="0d3a8-107">Se tradicional discos rígidos virtuais (VHD) foram usados para Kafka, cada nó está limitado too1 TB.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="0d3a8-108">Com discos gerenciados, você pode usar vários tooachieve de discos 16 TB para cada nó no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="0d3a8-109">Olá diagrama a seguir fornece uma comparação entre Kafka no HDInsight antes de discos gerenciados e Kafka no HDInsight com discos gerenciados:</span><span class="sxs-lookup"><span data-stu-id="0d3a8-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagrama mostrando o Kafka no HDInsight usando um único vhd por vm versus vários discos gerenciados por vm](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="0d3a8-111">Configurar discos gerenciados: portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0d3a8-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="0d3a8-112">Siga as etapas de Olá Olá [criar um cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand Olá comuns etapas toocreate um cluster usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="0d3a8-113">Não conclua o processo de criação de portal hello.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="0d3a8-114">De saudação __tamanho do Cluster__ folha, use Olá __discos por nó de trabalho__ tooconfigure Olá número de discos do campo.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0d3a8-115">Olá tipo de disco gerenciado pode ser __padrão__ (HDD) ou __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="0d3a8-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="0d3a8-116">Os discos Premium são usados com as VMs das séries DS e GS.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="0d3a8-117">Todos os outros tipos VM usam o padrão.</span><span class="sxs-lookup"><span data-stu-id="0d3a8-117">All other VM types use standard.</span></span>

    ![Imagem da folha de tamanho de cluster Olá com discos Olá por nó de trabalho realçado](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="0d3a8-119">Configurar discos gerenciados: modelo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="0d3a8-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="0d3a8-120">número de saudação do toocontrol de discos usados por nós de trabalho Olá em um cluster de Kafka, use Olá seção Olá modelo a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d3a8-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="0d3a8-121">Você pode encontrar um modelo completo que demonstra como tooconfigure gerenciada discos em [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="0d3a8-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d3a8-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d3a8-122">Next steps</span></span>

<span data-ttu-id="0d3a8-123">Para obter mais informações sobre como trabalhar com Kafka no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d3a8-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="0d3a8-124">Use MirrorMaker toocreate uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d3a8-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="0d3a8-125">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d3a8-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="0d3a8-126">Usar o Apache Spark com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="0d3a8-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="0d3a8-127">Conecte-se tooKafka por meio de uma rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="0d3a8-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="0d3a8-128">Blog do HDInsight em discos gerenciados com o Kafka</span><span class="sxs-lookup"><span data-stu-id="0d3a8-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)