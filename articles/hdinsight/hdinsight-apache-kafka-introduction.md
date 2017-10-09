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
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Introdução ao Apache Kafka no HDInsight (visualização)

[Apache Kafka](https://kafka.apache.org) é uma plataforma de streaming distribuído código-fonte aberto que pode ser usadas em tempo real de toobuild streaming pipelines de dados e aplicativos. Kafka também fornece o agente de mensagem funcionalidade semelhante tooa fila de mensagens, onde você pode publicar e assinar toonamed fluxos de dados. Kafka no HDInsight fornece um serviço gerenciado, altamente disponível e altamente escalonável na nuvem do Microsoft Azure hello.

## <a name="why-use-kafka-on-hdinsight"></a>Por que usar o Kafka no HDInsight?

Kafka fornece Olá recursos a seguir:

* Padrão de mensagens de publicação / assinatura: Kafka fornece uma API de produtor para publicar registros tooa tópico Kafka. Olá API de consumidor é usado durante a assinatura de tópico tooa.

* Processamento de fluxo: o Kafka é frequentemente usado com o Apache Storm ou o Spark para processamento de fluxo em tempo real. Kafka 0.10.0.0 (HDInsight versão 3.5) introduziu uma API de streaming que permite que você toobuild streaming soluções sem a necessidade de tempestade ou Spark.

* Escala horizontal: Kafka particiona fluxos em nós de saudação no cluster do HDInsight hello. Processos de consumidor podem ser associados a partições individuais tooprovide balanceamento de carga durante o consumo de registros.

* Entrega em ordem: dentro de cada partição, os registros são armazenados no fluxo de saudação na ordem de saudação que foram recebidos. Ao associar um processo do consumidor por partição, você pode garantir que os registros sejam processados na ordem.

* Tolerância: Partições podem ser replicadas entre a tolerância a falhas de tooprovide nós.

* Integração com o Azure gerenciados discos: discos gerenciado fornece maior escala e taxa de transferência para discos de saudação usados nas máquinas virtuais no cluster do HDInsight Olá Olá.

    Discos gerenciados são habilitados por padrão para Kafka no HDInsight e número de saudação de discos usados por nó pode ser configurado durante a criação de HDInsight. Para saber mais sobre discos gerenciados, veja [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).

    Para saber mais sobre como configurar discos gerenciados com o Kafka no HDInsight, veja [Aumentar a escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md).

## <a name="use-cases"></a>Casos de uso

* **Mensagens**: uma vez que ele dá suporte a saudação padrão de mensagens de publicação / assinatura, Kafka geralmente é usada como um agente de mensagens.

* **Atividade de controle**: Kafka desde que fornece o registro em log na ordem de registros, pode ser usado tootrack e crie novamente as atividades. Por exemplo, as ações do usuário em um site ou em um aplicativo.

* **Agregação**: usando processamento de fluxo, você pode agregar informações de fluxos diferentes toocombine e centralizar Olá informações em dados operacionais.

* **Transformação**: usando processamento de fluxo, você pode combinar e enriquecer dados de vários tópicos de entrada em um ou mais tópicos de saída.

## <a name="next-steps"></a>Próximas etapas

Links a seguir do uso Olá toolearn como toouse Kafka do Apache no HDInsight:

* [Introdução ao Kafka no HDInsight](hdinsight-apache-kafka-get-started.md)

* [Use MirrorMaker toocreate uma réplica de Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)

* [Usar Apache Storm com Kafka no HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Usar o Apache Spark com o Kafka no HDInsight](hdinsight-apache-spark-with-kafka.md)

* [Conecte-se tooKafka por meio de uma rede Virtual do Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
