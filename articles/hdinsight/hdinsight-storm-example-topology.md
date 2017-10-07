---
title: topologias do Apache Storm aaaExample no HDInsight | Microsoft Docs
description: "Uma lista das topologias de exemplo do Storm criadas e testadas com o Apache Storm no HDInsight, incluindo topologias básicas C# e Java e trabalho com os Hubs de Eventos."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Exemplo de topologias e componentes Storm para o Apache Storm no HDInsight

a seguir Olá é uma lista de exemplos criado e mantido pela Microsoft para uso com o Apache Storm no HDInsight. Esses exemplos abrangem uma variedade de tópicos, desde a criação básica c# e Java topologias tooworking com serviços do Azure, como Hubs de eventos, banco de dados do Cosmos, Power BI, banco de dados SQL, HBase em HDInsight e o armazenamento do Azure. Alguns exemplos também demonstram como toowork com tecnologias não são Azure ou até mesmo não sejam da Microsoft, como SignalR e Socket.IO.

| Descrição | Demonstra | Estrutura/linguagem |
|:--- |:--- |:--- |
| [Gravar repositório tooAzure Data Lake do Apache Storm](hdinsight-storm-write-data-lake-store.md) |Gravando repositório tooAzure Data Lake |Java |
| [Origem do Bolt e Spout do Hub de Eventos](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Fonte da saudação Spout do Hub de eventos e raio |Java |
| [Desenvolver topologias baseadas em Java para o Apache Storm no HDInsight][5797064f] |Maven |Java |
| [Desenvolver topologias do C# para o Apache Storm no HDInsight usando o Visual Studio][16fce2d1] |Ferramentas do HDInsight para Visual Studio |C#, Java |
| [Criar vários fluxos de dados em uma topologia Storm do C#][ec5a4064] |Vários fluxos |C# |
| [Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (C#)][844d1d81] |Hubs de Eventos |C# e Java |
| [Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Hubs de Eventos |Java |
| [Usar dados do Power Bi toovisualize de uma topologia Storm][94d15238] |Power BI |C# |
| [Analisando dados de sensor com o Storm e o HBase no HDInsight][ab894747] |Hubs de Evento, HBase, Socket.IO, painel da Web |C#, Java, JavaScript, HTML |
| [Processar dados de sensor do veículo nos Hubs de Eventos usando o Storm no HDInsight][246ee964] |Hubs de Eventos, Cosmos DB, WASB (Azure Storage Blob) |C#, Java |
| [Extração, transformação e carregamento (ETL) de tooHBase de Hubs de eventos do Azure, usando Storm no HDInsight][b4b68194] |Hubs de Evento, HBase |C# |
| [Projeto de modelo de topologia Storm do C# para trabalhar com os serviços do Azure por meio do Storm no HDInsight][ce0c02a2] |Hubs de Eventos, Cosmos DB, Banco de Dados SQL, HBase, SignalR |C#, Java |
| [Parâmetros de comparação de escalabilidade para leitura nos Hubs de Eventos do Azure usando o Storm no HDInsight][d6c540e3] |Taxa de transferência de mensagem, Hubs de Evento, Banco de Dados SQL |C#, Java |
| [Correlacionar eventos usando Storm e HBase no HDInsight](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Use o Python com o Storm em HDInsight](hdinsight-storm-develop-python-topology.md) |Componentes do Python com uma topologia Flux |Python |
| [Usar o Kafka com o Storm no HDInsight](hdinsight-apache-storm-with-kafka.md) | Leitura do Apache Storm e gravando tooApache Kafka | Java |

### <a name="next-steps"></a>Próximas etapas

* [Introdução ao Apache Storm no HDInsight][2b8c3488]
* [Saiba como toodeploy e gerenciar topologias Storm com Storm no HDInsight][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Saiba como toocreate uma profusão de cluster HDInsight e uso Olá topologias de exemplo do painel Storm toodeploy."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Saiba como toodeploy e gerenciar topologias usando Olá baseado na web profusão de painel e profusão de interface do usuário ou ferramentas do HDInsight Olá para o Visual Studio."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Saiba como topologias de C# Storm toocreate usando Olá ferramentas HDInsight para Visual Studio."
[5797064f]: hdinsight-storm-develop-java-topology.md "Saiba como topologias de profusão de toocreate em Java, usando o Maven, criando uma topologia de wordcount básico."
[94d15238]: hdinsight-storm-power-bi-topology.md "Demonstra como toowrite dados tooPower BI de uma topologia de c#, em seguida, criar um gráfico e o painel de dados de saudação."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Demonstra uma topologia Storm básica que executa uma contagem de palavras, implementada em C#. Isso também demonstra como toocreate vários fluxos de dados dentro de uma topologia c#."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Saiba como tooread e gravar dados de Hubs de eventos do Azure com Storm no HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Saiba como visualizá-la usando D3.js toouse Apache Storm no HDInsight tooprocess os dados do sensor de Hubs de eventos do Azure e (opcionalmente), armazene-a tooHBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Saiba como a toouse mensagens de tooread de topologia uma profusão de Hubs de eventos do Azure, leia os documentos do banco de dados do Azure Cosmos para fazer referência a dados e salvar dados tooAzure armazenamento."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Várias topologias toodemonstrate taxa de transferência ao ler de Hubs de eventos do Azure e armazenar tooSQL banco de dados usando o Apache Storm no HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Saiba como Hubs de eventos do Azure, agregação e transformar dados tooread Olá dados, em seguida, armazenam tooHBase no HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Este projeto contém modelos para toointeract spouts, parafusos e topologias com vários serviços do Azure, como Hubs de eventos, Cosmos banco de dados e banco de dados SQL."

