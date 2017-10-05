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
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Introdução ao Apache Kafka no HDInsight (visualização)

O [Apache Kafka](https://kafka.apache.org) é uma plataforma de streaming distribuída de software livre que pode ser usada para compilar pipelines e aplicativos de dados de streaming em tempo real. O Kafka também fornece funcionalidade de agente de mensagem semelhante a uma fila de mensagens, onde você pode publicar e assinar os fluxos de dados nomeados. O Kafka no HDInsight oferece um serviço gerenciado, altamente escalonável e altamente disponível na nuvem do Microsoft Azure.

## <a name="why-use-kafka-on-hdinsight"></a>Por que usar o Kafka no HDInsight?

O Kafka fornece as seguintes funcionalidades:

* Padrão de mensagens publicar-assinar: o Kafka fornece uma API de Produtor para publicação de registros em um tópico do Kafka. A API de Consumidor é usada na assinatura de um tópico.

* Processamento de fluxo: o Kafka é frequentemente usado com o Apache Storm ou o Spark para processamento de fluxo em tempo real. O Kafka 0.10.0.0 (HDInsight versão 3.5) introduziu uma API de streaming que permite que você crie soluções de transmissão sem a necessidade do Storm ou do Spark.

* Escala horizontal: o Kafka particiona fluxos entre os nós no cluster HDInsight. Os processos do Consumidor podem ser associados a partições individuais para fornecer balanceamento de carga ao consumir registros.

* Entrega em ordem: dentro de cada partição, os registros são armazenados no fluxo na ordem em que foram recebidos. Ao associar um processo do consumidor por partição, você pode garantir que os registros sejam processados na ordem.

* Tolerante a falhas: as partições podem ser replicadas entre nós para fornecer tolerância a falhas.

* Integração com os Azure Managed Disks: os discos gerenciados fornecem maior escala e taxa de transferência para os discos usados pelas máquinas virtuais no cluster HDInsight.

    Os discos gerenciados são habilitados por padrão para o Kafka no HDInsight e o número de discos usados por nó pode ser configurado durante a criação do HDInsight. Para saber mais sobre discos gerenciados, veja [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).

    Para saber mais sobre como configurar discos gerenciados com o Kafka no HDInsight, veja [Aumentar a escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md).

## <a name="use-cases"></a>Casos de uso

* **Mensagens**: já que ele oferece suporte ao padrão de mensagem publicar-assinar, o Kafka geralmente é usado como um agente de mensagem.

* **Rastreamento de atividades**: como o Kafka oferece o registro em log ordenado de registros, pode ser usado para rastrear e recriar as atividades. Por exemplo, as ações do usuário em um site ou em um aplicativo.

* **Agregação**: usando processamento de fluxo, você pode agregar informações de fluxos diferentes para combinar e centralizar as informações em dados operacionais.

* **Transformação**: usando processamento de fluxo, você pode combinar e enriquecer dados de vários tópicos de entrada em um ou mais tópicos de saída.

## <a name="next-steps"></a>Próximas etapas

Use os links a seguir para aprender a usar o Apache Kafka no HDInsight:

* [Introdução ao Kafka no HDInsight](hdinsight-apache-kafka-get-started.md)

* [Usar MirrorMaker para criar uma réplica de Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)

* [Usar Apache Storm com Kafka no HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Usar o Apache Spark com o Kafka no HDInsight](hdinsight-apache-spark-with-kafka.md)

* [Conectar-se ao Kafka no HDInsight (preview) por meio de uma Rede Virtual do Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)