---
title: "dados do sensor do veículo aaaProcess com Apache Storm no HDInsight | Microsoft Docs"
description: "Saiba como dados do sensor do veículo tooprocess dos Hubs de eventos usando o Apache Storm no HDInsight. Adicionar dados de modelo de banco de dados do Azure Cosmos e armazenar toostorage de saída."
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Processar dados de sensor de veículo nos Hubs de Eventos do Azure usando o Apache Storm no HDInsight

Saiba como dados de sensor de veículo tooprocess de Hubs de eventos do Azure usando o Apache Storm no HDInsight. Este exemplo lê dados do sensor de Hubs de eventos do Azure, enriquece dados saudação fazendo referência a dados armazenados no banco de dados do Azure Cosmos. Olá dados são armazenados no armazenamento do Azure usando Olá sistema de arquivo do Hadoop (HDFS).

![HDInsight e hello diagrama de arquitetura de Internet das coisas (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Visão geral

Adicionar sensores toovehicles permite toopredict problemas de equipamento com base nas tendências de dados históricos. Ele também permite que você toomake melhorias versões toofuture com base na análise de padrão de uso. Você deve ser capaz de tooquickly e carregar com eficiência dados saudação de todos os veículos no Hadoop antes que ocorra o processamento de MapReduce. Além disso, talvez você queira toodo análise para caminhos de falha crítica (temperatura de mecanismo, freios, etc.) em tempo real.

Hubs de eventos do Azure é construído toohandle Olá imenso volume de dados gerados por sensores. Apache Storm pode ser usado tooload e dados de saudação do processo antes de armazená-lo no HDFS.

## <a name="solution"></a>Solução

Os dados telemétricos de temperatura do mecanismo, temperatura ambiente e velocidade do veículo são registrados pelos sensores. Dados são enviados, em seguida, Hubs tooEvent juntamente com veículo identificação número VIN do carro Olá () e um carimbo de hora. A partir daí, uma topologia de Storm em execução em um Apache Storm no cluster HDInsight lê dados hello, processa e armazena-o no HDFS.

Durante o processamento, Olá VIN é usado tooretrieve informações sobre o modelo do banco de dados do Cosmos. Esses dados são adicionados toohello fluxo de dados antes de ser armazenado.

Olá componentes usados em Olá profusão de topologia são:

* **EventHubSpout** - lê dados de Hubs de Evento do Azure
* **TypeConversionBolt** -Olá converte a cadeia de caracteres JSON dos Hubs de eventos em uma tupla que contém a saudação seguintes dados de sensor:
    * Temperatura do motor
    * Temperatura ambiente
    * Velocidade
    * VIN
    * Timestamp
* **DataReferencBolt** -procura o modelo do veículo saudação do banco de dados do Cosmos usando VIN Olá
* **WasbStoreBolt** -Olá de repositórios de dados tooHDFS (armazenamento do Azure)

Olá a imagem a seguir é um diagrama da solução:

![topologia Storm](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Implementação

Uma completa solução automatizada para esse cenário está disponível como parte da saudação [HDInsight de profusão de exemplos](https://github.com/hdinsight/hdinsight-storm-examples) repositório no GitHub. toouse neste exemplo, siga etapas Olá Olá [IoTExample README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Próximas etapas

Para obter mais topologias do Storm, consulte [Exemplo de topologias para Storm em HDInsight](hdinsight-storm-example-topology.md).

