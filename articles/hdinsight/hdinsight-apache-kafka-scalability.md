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
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Configurar o armazenamento e a escalabilidade para o Apache Kafka no HDInsight

Saiba como número de saudação tooconfigure de discos gerenciados usados pelo Apache Kafka no HDInsight.

Kafka no HDInsight usa a disco local Olá de máquinas virtuais de saudação no cluster do HDInsight hello. Como Kafka é bastante e/s pesados, [discos gerenciado do Azure](../virtual-machines/windows/managed-disks-overview.md) é usado tooprovide alta taxa de transferência e fornece mais armazenamento por nó. Se tradicional discos rígidos virtuais (VHD) foram usados para Kafka, cada nó está limitado too1 TB. Com discos gerenciados, você pode usar vários tooachieve de discos 16 TB para cada nó no cluster hello.

Olá diagrama a seguir fornece uma comparação entre Kafka no HDInsight antes de discos gerenciados e Kafka no HDInsight com discos gerenciados:

![Diagrama mostrando o Kafka no HDInsight usando um único vhd por vm versus vários discos gerenciados por vm](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Configurar discos gerenciados: portal do Azure

1. Siga as etapas de Olá Olá [criar um cluster HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand Olá comuns etapas toocreate um cluster usando o portal de saudação. Não conclua o processo de criação de portal hello.

2. De saudação __tamanho do Cluster__ folha, use Olá __discos por nó de trabalho__ tooconfigure Olá número de discos do campo.

    > [!NOTE]
    > Olá tipo de disco gerenciado pode ser __padrão__ (HDD) ou __Premium__ (SSD). Os discos Premium são usados com as VMs das séries DS e GS. Todos os outros tipos VM usam o padrão.

    ![Imagem da folha de tamanho de cluster Olá com discos Olá por nó de trabalho realçado](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Configurar discos gerenciados: modelo do Gerenciador de Recursos

número de saudação do toocontrol de discos usados por nós de trabalho Olá em um cluster de Kafka, use Olá seção Olá modelo a seguir:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Você pode encontrar um modelo completo que demonstra como tooconfigure gerenciada discos em [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como trabalhar com Kafka no HDInsight, consulte Olá documentos a seguir:

* [Use MirrorMaker toocreate uma réplica de Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Usar Apache Storm com Kafka no HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Usar o Apache Spark com o Kafka no HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Conecte-se tooKafka por meio de uma rede Virtual do Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Blog do HDInsight em discos gerenciados com o Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)