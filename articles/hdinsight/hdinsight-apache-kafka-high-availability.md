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
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>Alta disponibilidade de seus dados com o Apache Kafka (versão prévia) no HDInsight

Saiba como réplicas da partição tooconfigure para Kafka tópicos tootake aproveitar hardware subjacente rack configuração. Essa configuração garante a disponibilidade de saudação dos dados armazenados no Apache Kafka no HDInsight.

## <a name="fault-and-update-domains-with-kafka"></a>Domínios de falha e atualização com Kafka

Um domínio de falha é um agrupamento lógico de hardware subjacente em um data center do Azure. Cada domínio de falha tem um comutador de rede e uma fonte de alimentação em comum. máquinas virtuais de saudação e discos gerenciados que implementa nós hello dentro de um cluster HDInsight são distribuídos entre esses domínios de falha. Essa arquitetura limita o impacto potencial de saudação de falhas de hardware físico.

Cada região do Azure tem um número específico de domínios de falha. Para obter uma lista de domínios e número de saudação de domínios de falha que eles contêm, consulte Olá [conjuntos de disponibilidade](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentação.

> [!IMPORTANT]
> O Kafka não está ciente dos domínios de falha. Quando você cria um tópico no Kafka, ele pode armazenar todas as réplicas de partição em Olá mesmo domínio de falha. toosolve esse problema, fornecemos Olá [ferramenta de rebalanceie de partição Kafka](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Quando toorebalance réplicas da partição

tooensure hello mais alta disponibilidade de seus dados Kafka, você deve reequilibrar réplicas da partição Olá para seu tópico em Olá vezes a seguir:

* Quando um novo tópico ou uma partição é criado

* Quando você expande um cluster

## <a name="replication-factor"></a>Fator de replicação

> [!IMPORTANT]
> É recomendável usar uma região do Azure que contenha três domínios de falha e um fator de replicação de 3.

Se você precisar usar uma região que contém apenas dois domínios de falha, use um fator de replicação de 4 réplicas de saudação toospread uniformemente entre os dois domínios de falha hello.

Para obter um exemplo de criação de tópicos e o fator de replicação de saudação de configuração, consulte Olá [iniciar com Kafka no HDInsight](hdinsight-apache-kafka-get-started.md) documento.

## <a name="how-toorebalance-partition-replicas"></a>Como a partição toorebalance réplicas

Saudação de uso [ferramenta de rebalanceie de partição Kafka](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selecionado tópicos. Essa ferramenta deve ser executado de um nó SSH sessão toohello principal do cluster Kafka.

Para obter mais informações sobre como conectar tooHDInsight usando SSH, consulte o [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

## <a name="next-steps"></a>Próximas etapas

* [Escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md)
* [Espelhamento com o Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)